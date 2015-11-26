# spider
在nodel里面安装cheerio和request依赖。然后对豆瓣电影的内容进行爬取。

###cheerio:可以跟jquery一样操作 中文版操作手册：https://cnodejs.org/topic/5203a71844e76d216a727d2e

    //爬取豆瓣电影每周口碑榜的十条数据
    var express = require('express');
    var app = express();
    var request = require('request');
    var cheerio = require('cheerio');
    
    app.get('/', function(req, res) {
      request('http://movie.douban.com/', function(error, response, body) {
        if(!error && response.statusCode == 200){
          var $ = cheerio.load(body);
          var lists = $("td.title a");
          var arr = [];
          lists.each(function() {
            arr.push($(this).text());
          });
          res.send(arr);
        }
      })
    });
    
    app.listen(3000);
    
###该demo只是小试牛刀，实际爬取过程中还需要遵守robots协议，以及对爬虫的优化，考虑ajax请求到的数据等。。。
