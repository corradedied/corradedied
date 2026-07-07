Good catch, and you're right that it wasn't working as a queue.

`MaxNotifications` defaults to 10, and the loop fires all 15 `Notify()` calls in the same frame with nothing yielding between them. The old code inserted each new notification then immediately destroyed the oldest one past the cap - so 1 through 5 got created and torn down before a single frame ever rendered. `NotificationQueue` was really just a hard concurrency cap with instant eviction, not a queue.

I've reworked it so overflow notifications go into a `PendingNotifications` list instead of spawning (and getting destroyed) immediately. When an active notification expires and frees a slot, the next pending one gets spawned. Your test case now shows 1-10 right away, then 11-15 roll in one at a time as each of the first ten times out.

On the yielding concern - I looked through the call path and don't see an actual coroutine yield in `SetMaxNotifications` or the eviction logic; `Destroy()` only uses non-blocking tweens and `task.delay`. If you saw something specific yielding, let me know where and I'll take another look.

With actual queuing in place, does that change your view on keeping `SetMaxNotifications`, or do you still think it's not worth having?
<img width="272" height="1072" alt="ezgif-4426fec2c102c2f8" src="https://github.com/user-attachments/assets/e3407cb9-c0c6-4e53-9014-fc47f42a70f8" />
