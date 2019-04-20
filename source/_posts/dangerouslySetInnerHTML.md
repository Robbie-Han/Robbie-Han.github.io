---
title: dangerouslySetInnerHTML
tags: 
- React
---
### dangerouslySetInnerHTML在react和redux中的应用

```
<div dangerouslySetInnerHTML={{__html: "<p>balabalabalabala.......</p><p>balalababalalaba....</p>"}} />
<div dangerouslySetInnerHTML={{__html: props.modalContent}}/>
```

功能将__html后的内容嵌套到div下