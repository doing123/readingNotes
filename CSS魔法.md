原生currentColor：与color一致，本身就是很多 CSS 颜色属性的初始值，比如border-color 和 outline-color，以及 text-shadow 和 box-shadow 的颜 色值，等等

视口相关的单位(vw、vh、vmin 和 vmax)

background: url(tr.png) no-repeat top right / 2em 2em,url(br.png) no-repeat bottom right / 2em 2em,
            url(bl.png) no-repeat bottom left / 2em 2em;


background: url(tr.png) top right,url(br.png) bottom right,
url(bl.png) bottom left;background-size: 2em 2em;
background-repeat: no-repeat;

原生变量：var 
body{
--深蓝: #369;
background-color: var(--深蓝);
}

background: url(code-pirate.svg) no-repeat bottom right #58a;
background-position: right 20px bottom 10px;

background-origin: content-box; // border-box; padding-box;

background: linear-gradient(#fb3 33.3%, // to bottom默认； to right:90deg
#58a 0, #58a 66.6%, yellowgreen 0);
background-size: 100% 45px; // 在后才有效果

clip-path:裁剪路径方案

transform: perspective(.5em) rotateX(5deg);
perspective 属性定义 3D 元素距视图的距离，以像素计。该属性允许您改变 3D 元素查看 3D 元素的视图。

transform: rotate(.1turn); // 1turn = 360度

filter: drop-shadow(2px 2px 10px rgba(0,0,0,.5));

hyphens: auto; // 连字符断行

dt::before {content: '\A'; // 插入换行
white-space: pre; }

tab-size: 2; // 调整tab的宽度

max-width: min-content; // 这个关键字将解析为这个容器内 部最大的不可断行元素的宽度(即最宽的单词、图片或具有固定宽度的盒元 素)

animation: loader 1s infinite steps(8);  // 逐帧动画