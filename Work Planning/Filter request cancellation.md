- have abort controller 
```typescript
const controller = new AbortController();
this.http.get('/api/data', { signal: controller.signal }).subscribe();
controller.abort();
```

```c#
[HttpGet]
public async Task<IActionResult> GetData(CancellationToken cancellationToken)
{
    try
    {
        // Respect the cancellation
        await Task.Delay(10000, cancellationToken);
        return Ok("done");
    }
    catch (OperationCanceledException)
    {
        // Cleanly handle cancellation
        return StatusCode(StatusCodes.Status499ClientClosedRequest);
    }
}
```

possibly return Http 499(client cancelled request)