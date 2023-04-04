# CSS选择器

## 1.标示选择器

只能使用一次

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>选择器</title>
    <style>
        p {
            color: rgb(182, 77, 77);
            font-family: "宋体";
            font-style: italic;
        }
    </style>
</head>
<body>
    <p>wfawjifowwaf</p>
</body>
</html>
```

## 2.类名选择器

可以多次使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>选择器</title>
    <style>
        .div_1 {
            color: red;
        }
    </style>
</head>
<body>
    <p class="div_1">asoijfowjfoa</p>
</body>
</html>
```

## 3.id选择器

只能使用一次

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>选择器</title>
    <style>
        #body1 {
            font-size: medium;
            font-weight: bolder;
        }
    </style>
</head>
<body>
    <p id="body1">aojfwoijfoaw</p>
</body>
</html>
```

## 4.通配符选择器

匹配页面中所有的元素

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>选择器</title>
    <style>
        * {
            font-size: medium;
            font-weight: bolder;
        }
    </style>
</head>
<body>
    <p>aojfwoijfoaw</p>
</body>
</html>
```

## 5.标签指定式选择器

## 6.后代选择器

前提：元素之间要有后代关系

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>选择器</title>
    <style>
        p b {
            font-size: medium;
            font-weight: bolder;
            color: yellow;
        }
    </style>
</head>
<body>
    <p>
        所钢琴文职盖哦古玩蜂<b>佛号</b>窝家三奥小我
    </p>
</body>
</html>
```

## 7.并集选择器

选择器和选择器之间用逗号隔开

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>选择器</title>
    <style>
        h1,h2 {
            font-size: medium;
            font-weight: bolder;
            color: yellow;
        }
    </style>
</head>
<body>
    <h1>实现一级标题字体加粗bold</h1>
    <h2>实现二级标题字体设置宋体</h2>
</body>
</html>
```
