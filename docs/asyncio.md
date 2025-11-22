# Asyncio

## High-Level

* Event loop
* Coroutine Functions
* Coroutine Objects
* Tasks
* `await`

### Event Loop

The Event Loop contains a collection of jobs to be run.  
Some jobs are added by the user and some indirectly by asyncio.  
The event loop takes a job from its backlog of work and invokes it, similar to calling a function and then that job runs.  
Once it pauses or completes, it returns control to the event loop.  
The event loop will select another job from its pool and invoke it.  

* Effective execution often relies on jobs sharing well and cooperating.
```python
import asyncio

# This creates an event loop and indefinitely cycles through
# its collection of jobs.
event_loop = asyncio.new_event_loop()
event_loop.run_forever()
```
### Asynchronous functions and Coroutines

The async def, as opposed to just a plain def, makes this an asynchronous function (or “coroutine function”).  
Calling it creates and returns a coroutine object.  

