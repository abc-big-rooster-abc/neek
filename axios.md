# axios

## jsonP

~~~js
let count = 1
export default function originJsonP(option){
    // 1.从传入的option中提取url
    const url = option.url;

    // 2.在bodY中添加script标签
    const  body = document.getElementsByTagName('body')[0];
    const script = document.createElement('script');
    // 3.内部生产一个不重复的callback
    const callback = 'jsonp' + count++;
    // 4.监听window上的jsonp的调用
    return new Promise((resolve,reject)=>{
        try{
            window[callback] = function(result){
                body.removeChild(script);
                resolve(result)
            }
            const params = handleParam(option.data);
            script.src = url + "?callback=" + callback + params;
            body.appendChild(script);
        } catch(e){
            body.removeChild(script)
            reject(e)
        }
    })
}


function handleParam(data){
    let url = '';
    for(let key in data){
        let value = data[key] !== undefined ? data[key] : ''
        url += `&${key}=${encodeURIComponent(value)}`
    }
    return url
}
~~~







## axios

~~~js
import axios from 'axios'

export default {
    name: "app",
    created(){
        axios.get("http://123.207.32.32:8000/catepory")
        .then(res=>{
            console.log(res);
        }).catch(err=>{
            console.log(err);
        })

        // 2.有请求参数
        axios.get("http://123.207.32.32:8000/home/data", {params:{type:"sell",page:1}
    })
    .then(res=>{
        console.log(res)
    }).catch(err=>{
        console.log(err)
    })
}
}
~~~

