# LRU

```go
type LRUCache struct {
	capacity int           // 容量
	cache    map[string]*list.Element // 缓存映射
	list     *list.List    // 双向链表
	mu       sync.Mutex    // 锁
}

type elem struct {
	key string
	val string
}

func NewLRUCache(c int) *LRUCache {
	return &LRUCache {
		capacity: c,
		cache: make(map[string]*list.Element),
		list: list.New()
	}
}

func (l *LRUCache) Get(k string) string {
	l.mu.Lock()
	defer l.mu.Unlock()
	
	if v, ok := l.cache[k]; ok {
		// 移到队首
		l.list.MoveToFront(v)
		
		// 返回结果
		return v.Value.(*elem).val
	}
	
	return ""
}

func (l *LRUCache) Put(k, v string) {
	l.mu.Lock()
	defer l.mu.Unlock()
	
	// 如果存在，则更新值，并且移到队首
	if ele, ok := l.cache[k]; ok {
		// 移到队首
		l.list.MoveToFront(ele)
		
		// 更新值
		v.Value.(*entry).val = v
		
		return
	}
	
	// 不存在先截断容量
	if len(l.cache) >= capacity {
		ele := l.list.Back()
		delete(l.cache, ele.Value.(*elem).key)
		l.list.Remove(ele)
		l.capa
	}
	
	// 写入队首
	l.list.PushFront(*elem{
		key: k,
		val: v
	})
	l.cache[k] = l.list.Front()
	
}

func (l *LRUCache) Keys() []string {
	l.mu.Lock()
	defer l.mu.Unlock()
	
	res := make([]string, 0, len(l.cache))
	for ele := l.list.Front(); ele != nil {
		res = append(res, ele.Value.(*elem).key)
		ele = ele.Next()
	}
	
	return res
}

func (l *LRUCache) Clear() {
	l.mu.Lock()
	defer l.mu.Unlock()
	
	l.cache = make(map[string]*list.Element)
	l.list = list.New()
	return
}

```

---
创建时间: 2026-01-16 16:12
标签: #concept
