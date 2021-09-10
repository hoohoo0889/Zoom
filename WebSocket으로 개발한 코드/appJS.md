const messageList = document.querySelector("ul");
const messageForm = document.querySelector("#message");
const nickForm = document.querySelector("#nick");
const myNickName = document.querySelector("#myNickName");
const socket = new WebSocket(`ws://${window.location.host}`);

function makeMessage(type, payload) {
const msg = { type, payload };
return JSON.stringify(msg);
}

socket.addEventListener("open", () => {
console.log("Connected to Server");
});

socket.addEventListener("message", (message) => {
const li = document.createElement("li");
li.innerText = message.data;
messageList.append(li);
});

socket.addEventListener("close", () => {
console.log("Dsiconnected from Server");
});

function handleSubmit(event) {
event.preventDefault();
const input = messageForm.querySelector("input");
socket.send(makeMessage("new_message", input.value));
input.value = "";
}

function handleNickSubmit(event) {
event.preventDefault();
input = nickForm.querySelector("input");
myNickName.innerText += ` ${input.value}`;
socket.send(makeMessage("nickname", input.value));
input.value = "";
}

messageForm.addEventListener("submit", handleSubmit);
nickForm.addEventListener("submit", handleNickSubmit);
