---
title: 我的第网页
---

# {{ page.title }}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title># {{ page.title }}</title>
    <style>
        *{
            padding:0;
            margin:0;
        }
        .cbox{
            position: absolute;
            left:0;
            top:0;
            width:80px;
            height:80px;
            -webkit-border-radius:50%;
            -moz-border-radius:50%;
            border-radius:50%;
            background: #000;
        }
    </style>
</head>
<body>
  <div id="box" class="cbox"></div>
</body>
<script>
    var Body=document.getElementsByTagName("body")
    var Div=document.getElementById('box');
    var stop=0;
    var sleft=0;
//    var Hbool=true;
//    var Wbool=true;
    var arr=[0,1,2,3,4,5,6,7,8,9,'A','B','C','D','E','F'];
    var aDiv=[];

    for(var i=0;i<4;i++){
        aDiv[i]=document.createElement("div");
        aDiv[i].className="cbox";
        aDiv[i].add=(i+1)*2;
        Body[0].appendChild(aDiv[i]);
        run(aDiv[i]).call(aDiv[i]);
    }
    //run(Div);
    function run(obj) {

        var width=parseFloat(getstyle(obj,"width"));
        var height=parseFloat(getstyle(obj,"height"));
        //var add=5;

        var Hbool=true;
        var Wbool=true;

        function fn() {
            var timer=setInterval(function () {

                var color='#';
                var Top=obj.offsetTop;
                var Left=obj.offsetLeft;
                var vWidth=document.documentElement.clientWidth;
                var vHeight=document.documentElement.clientHeight;
                for(var i=0;i<6;i++){
                    color+=arr[ Math.floor(Math.random()*17)];

                }
                if(Hbool){
                    console.log(stop)
                    stop=this.add+Top;
                    if((stop+height)>=vHeight){
                        Hbool=false;
                        stop=vHeight-height;
                        obj.style.backgroundColor=color;
                    }
                }else{
                    stop=Top-this.add;
                    if(stop<=0){
                        Hbool=true;
                        stop=0;
                        obj.style.backgroundColor=color;//在IE8下这句代码无效，不知道外什么，上面的这句代码却是有效的
                    }
                }
                if(Wbool){
                    sleft=this.add+Left;
                    if((sleft+height)>=vWidth){
                        Wbool=false;
                        sleft=vWidth-height;
                        obj.style.backgroundColor=color;
                    }
                }else{
                    sleft=Left-this.add;
                    if(sleft<=0){
                        Wbool=true;
                        sleft=0;
                        obj.style.backgroundColor=color;
                    }
                }
                obj.style.top=stop+"px";
                obj.style.left=sleft+"px";
            }.call(this),1000/60);
        }

        return fn;
    }

    function getstyle(obj,attr){
        return obj.currentStyle?obj.currentStyle[attr]:getComputedStyle(obj)[attr];
    }

</script>
</html>
