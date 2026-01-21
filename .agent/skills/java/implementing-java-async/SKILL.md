---
name: implementing-java-async
description: Implements `@Async` tasks and `@Scheduled` jobs with strict status tracking in the database.
---

# Implementing Java Async Tasks

## When to use this skill
- Long-running operations (STT, AI summarization, Email).
- Periodic background jobs.

## Principles (Strict)
1.  **Always Track Status**: Never run a void `@Async` without DB status updates.
    - Statuses: `PENDING` -> `PROCESSING` -> `COMPLETED`/`FAILED`.
2.  **CompletableFuture**: Return `CompletableFuture<T>` if result is needed.
3.  **Exception Handling**: Catch all exceptions inside the async method and update status to `FAILED`.
4.  **Transaction**: Async methods start a NEW transaction.

## Workflow

### 1. Async Service Method

```java
@Async
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void processVideo(Long videoId) {
    Video video = videoRepository.findById(videoId).orElseThrow();
    
    try {
        video.setStatus(VideoStatus.PROCESSING);
        
        // Long running task...
        externalApiService.process(video);
        
        video.setStatus(VideoStatus.COMPLETED);
    } catch (Exception e) {
        log.error("Async fail", e);
        video.setStatus(VideoStatus.FAILED);
    }
    // Auto-save via transaction dirtiness inside try/catch if managed, 
    // but better to save explicitly if catching generic Exception
    videoRepository.save(video); 
}
```

### 2. Scheduled Task

```java
@Scheduled(cron = "0 0 2 * * *") // 2 AM Daily
public void dailyCleanup() {
    // Logic
}
```

## Checklist
- [ ] Is `@EnableAsync` in a Config class?
- [ ] Does the async method return `void` or `CompletableFuture`?
- [ ] Is the database updated with status changes?
- [ ] Is there a `try-catch` block to handle failures gracefully?
