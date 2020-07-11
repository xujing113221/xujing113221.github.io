---
title: 文章热度排行
date: 2020-07-09 21:42:03
comments: false
---

<div id="post-rank">
  <p>This will be overwritten.</p>
</div>

<script src="//cdn.jsdelivr.net/npm/leancloud-storage@4.6.1/dist/av-min.js"></script>
<script>
  var APP_ID = '0HeenH1M6kEofmoCdXFMym4r-MdYXbMMI'  //输入个人LeanCloud账号AppID
  var APP_KEY = 'pLAfLofofkawWDO8zuponHLq'  //输入个人LeanCloud账号AppKey
  AV.init({
    appId: APP_ID,
    appKey: APP_KEY
  });

  var query = new AV.Query('Counter'); //表名
  query.descending('time');   //结果按阅读次数降序排序
  query.limit(10);          //最终只返回10条结果
  query.find().then( response => {
    var content = response.reduce( (accum, {attributes}) => {
      accum += `<p><div class="prefix">热度 ${attributes.time} ℃</div><div><a href="${attributes.url}">${attributes.title}</a></div></p>`
      return accum;
    },"")
    document.querySelector("#post-rank").innerHTML = content;
  })
  .catch( error => {
    console.log(error);
  });
</script>

<style type="text/css">
  #post-rank {
    text-align: center;
  }
  #post-rank .prefix {
    color: #ff4d4f;
  }
</style>