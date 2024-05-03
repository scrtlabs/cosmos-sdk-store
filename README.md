# Cosmos-sdk -> cosmossdk.io/store@v1.0.2
## cosmossdk.io/store@v1.0.2
The version of cosmossdk.io/store@v1.0.2 has an issue we have come across during the upgrade to Cosmoms-sdk 0.50.x
This issue is based on the fact that during the store __Write__ operation not every store gets updated.
As a result when we call 
```
func (rs *Store) CacheMultiStoreWithVersion(version int64) (types.CacheMultiStore, error)
```
a call to retrieve __cacheStore__ here:
```
cacheStore, err = store.(*iavl.Store).GetImmutable(version)
``` 
fails and we cannot process **multistore** queries because they fail with an error:
```

```
We introduced a fix for __CacheMultiStoreWithVersion__ where we bypass errors for certain modules.

