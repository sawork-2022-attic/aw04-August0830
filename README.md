# WebPos Report



Load testing with gatling.

1. no cache,no session, docker to get products.

![image-20220330210039797](https://gitee.com/mzl0830/pic-storage/raw/master/image-20220330210039797.png)

2. cache with redis cluster, no session, docker to get products

![image-20220331230829806](https://gitee.com/mzl0830/pic-storage/raw/master/image-20220331230829806.png)

After adding cache, it's faster to get products. Because other clients have access to data which has already stored in redis.



Horizontally scalable with four dockers with one cache based on redis cluster

![image-20220331230707733](https://gitee.com/mzl0830/pic-storage/raw/master/image-20220331230707733.png)

I suppose mean response time will be shorter after horizontally scalable with only one redis cluster. Because all the sub-server behind haproxy will share the same data in cache. However, it's slower. Maybe running four dockers once at a time makes it slower or it's affected by networking connection.



3. cache, session with one redis cluster and add a product for each client, not just view the products. 

Revised gatling environment:

```
.get("/add?pid=13284888"))
```

![image-20220401233259742](https://gitee.com/mzl0830/pic-storage/raw/master/image-20220401233259742.png)

We can see that it takes longer time. And redis cluster store those session information.

![image-20220401233347593](https://gitee.com/mzl0830/pic-storage/raw/master/image-20220401233347593.png)

It takes me quite a long time to prepare docker and redis cluster as well as figure out where I should add cache and how to set session. The problems I came across and the ways I figure them out are recorded [here](https://august0830.github.io/post/961e2082/)

