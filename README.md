# ajax
对于get请求和post请求的封装函数，以及兼容性问题考虑
分为几个步骤
1. 创建xhr对象和兼容性问题xhr = new XMLHttpRequest()
2. 准备发送请求open(type,url)
3. 创建回调函数，监测事件
4. 正式发送请求send(null)get为null，post为查询参数或具体的请求数据。

//创建get请求方法
function get(url,options,callback) {
  // 1.创建xhr对象和兼容性侦测
  if (XMLHttpRequest) {
      var xhr=new XMLHttpRequest();
    } else{
      var xhr=new ActiveXObject("Microsoft.XMLHTTP");//兼容ie6以下
    }

  // 2.发送请求
  var serurl = url + serialize(options); 
  open('get',serurl,true);
  //3.创建回调函数
  xhr.onreadystatechange = function(callback) {
    if (xhr.readyState == 4) {
      if (xhr.status >=200 & xhr.status < 300 || xhr.status == 304) {
        callback(xhr.responseText);
      } else {
        alert('Request Was unsuccessful: ' + xhr.status);
      }
    }
  } 
  //4.正式发送请求
  send(null);
}
  //5. 创建修改查询参数的函数封装
  function serialize(data) {
    if (!data) {return ""};
    var pais =[];
    for (var name is data) {
      if (!data.hasOwnProperty(name)) continue;
      if (typeof data[name] === 'function') continue;
      var value = data[name].toString();
      name =  encodeURIComponent(name);
      value = encodeURIComponent(value);
      pairs.push(name + '=' + value);
    }
    return pairs.join('&');
  }

  //创建post请求方法
  function post(url,options,callback) {
  // 1.创建xhr对象和兼容性侦测
  if (XMLHttpRequest) {
      var xhr=new XMLHttpRequest();
    } else{
      var xhr=new ActiveXObject("Microsoft.XMLHTTP");//兼容ie6以下
    }
  // 2.准备发送请求
  open('post',url,true);
  // 3.创建回调函数   
  xhr.onreadystatechange = function(callback) {
    if (xhr.readyState == 4) {
      if (xhr.status >=200 & xhr.status < 300 || xhr.status == 304) {
        callback(xhr.responseText);
      } else {
        alert('Request Was unsuccessful: ' + xhr.status);
      }
    }
  } 
  // 4.正式发送请求
  send(serialize(options));
}
  //5. 创建修改查询参数的函数封装
  function serialize(data) {
    if (!data) {return ""};
    var pais =[];
    for (var name is data) {
      if (!data.hasOwnProperty(name)) continue;
      if (typeof data[name] === 'function') continue;
      var value = data[name].toString();
      name =  encodeURIComponent(name);
      value = encodeURIComponent(value);
      pairs.push(name + '=' + value);
    }
    return pairs.join('&');
  }
