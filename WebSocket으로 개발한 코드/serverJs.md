import express from "express";
import http from "http";
import WebSocket from "ws";

const app = express();

app.set("view engine", "pug");
app.set("views", **dirname + "/views");
app.use("/public", express.static(**dirname + "/public"));
app.get("/", (_, res) => res.render("home"));
app.get("/\*", (_, res) => res.redirect("/"));

const handleListen = () => console.log(`Listening on http://localhost:3000`);

const server = http.createServer(app);
const wss = new WebSocket.Server({ server });

const sockets = [];

wss.on("connection", (socket) => {
sockets.push(socket);
socket["nickname"] = "Anon";
console.log("Connected to Broswer");
socket.on("close", () => console.log("Disconnected from Broswer"));
socket.on("message", (msg) => {
const message = JSON.parse(msg);
switch (message.type) {
case "new_message":
sockets.forEach((aSocket) =>
aSocket.send(`${socket.nickname}: ${message.payload}`)
);
break;
case "nickname":
socket["nickname"] = message.payload;
break;
}
});
});

server.listen(3000, handleListen);
