1. ?? 只过滤null / undefined

```
// before
const a = 0 || 6
// after
const a = 0 ?? 6
```

2. ?.()