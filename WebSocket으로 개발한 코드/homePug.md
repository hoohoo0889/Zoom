doctype html
html(lang="en")
head
meta(charset="UTF-8")
meta(http-equiv="X-UA-Compatible", content="IE=edge")
meta(name="viewport", content="width=device-width, initial-scale=1.0")
title ZOOM
link(rel="stylesheet", href="https://unpkg.com/mvp.css")
body
header
h1 JERIC ZOOM
main
p#myNickName 나의 닉네임 :
form#nick
input(type="text", placeholder="choose your nickname" required)
button Save
ul
form#message
input(type="text", placeholder="write a msg" required)
button Send
script(src="/public/js/app.js")
