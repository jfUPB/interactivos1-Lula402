### Server
```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');
const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };
let page3 = { x: 0, y: 0, width: 100, height: 100 };
let page4 = { x: 0, y: 0, width: 100, height: 100 };
let page5 = { x: 0, y: 0, width: 100, height: 100 };
let page6 = { x: 0, y: 0, width: 100, height: 100 };

app.use(express.static(path.join(__dirname, 'views')));

app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

app.get('/page2', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page2.html'));
});

app.get('/page3', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page3.html'));
});

app.get('/page4', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page4.html'));
});

app.get('/page5', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page5.html'));
});

app.get('/page6', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page6.html'));
});

io.on('connection', (socket) => {
    console.log('A user connected - ID:', socket.id); 
    socket.on('disconnect', () => {
        console.log('User disconnected - ID:', socket.id);
    });

    socket.on('win1update', (window1, sendid) => {
        console.log('Received win1update from ID:', socket.id, 'Data:', window1);
        page1 = window1;
        socket.broadcast.emit('getdata1', page1);
    })

    socket.on('win2update', (window2, sendid) => {
        console.log('Received win2update from ID:', socket.id, 'Data:', window2);
        page2 = window2;
        socket.broadcast.emit('getdata2', page2)
    })

    socket.on('win3update', (window3, sendid) => {
        console.log('Received win3update from ID:', socket.id, 'Data:', window3);
        page3 = window3;
        socket.broadcast.emit('getdata3', page3)
    })

       socket.on('win4update', (window4, sendid) => {
        console.log('Received win4update from ID:', socket.id, 'Data:', window4);
        page4 = window4;
        socket.broadcast.emit('getdata4', page4)
    })

      socket.on('win5update', (window5, sendid) => {
        console.log('Received win4update from ID:', socket.id, 'Data:', window5);
        page5 = window5;
        socket.broadcast.emit('getdata5', page5)
    })

     socket.on('win6update', (window6, sendid) => {
        console.log('Received win4update from ID:', socket.id, 'Data:', window6);
        page6 = window6;
        socket.broadcast.emit('getdata6', page6)
    })

});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});

```

### page1
```js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
}

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point1 = [currentPageData.width / 2, currentPageData.height / 2]

let socket = io('http://localhost:3000')
let speed=5;
let x= 0;

socket.on('connect', () => {
    console.log(socket.id);
    socket.emit('win1update', currentPageData, socket.id);
})


socket.on('getdata', (dataWindow) => {
    remotePageData = dataWindow;
})

let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};


function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
    x=0;
}


function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {

        point1 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win1update', currentPageData, socket.id);
        previousPageData = currentPageData;
    }
}


function draw() {
    checkWindowPosition();
    background(0);
    let y = height / 2;
    let startX = currentPageData.x;
    let localX = x - startX;

    x += speed;

    if (x > 1920 * 4 || x < 0) {
        speed *= -1;
    }

    if (localX >= 0 && localX <= width) {
         stroke(255, 0, 150);
        strokeWeight(8);
    line(localX, height / 2, localX + 40, height / 2);
}
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```

### page2
```js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight

}

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point2 = [currentPageData.width / 2, currentPageData.height / 2];
let socket = io('http://localhost:3000')
let speed=5;
let x= 0;

socket.on('connect', () => {
    console.log(socket.id);
    socket.emit('win2update', currentPageData, socket.id);
});

socket.on('getdata', (dataWindow) => {
    remotePageData = dataWindow;
    console.log(remotePageData);
});


let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};


function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
}


function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {
        console.log("Page 2 detected change, sending update:", currentPageData); 
        point2 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win2update', currentPageData, socket.id);
        previousPageData = currentPageData; 
    }
}


function draw() {
  checkWindowPosition();
    background(0);
    let y = height / 2;
    let startX = currentPageData.x;
    let localX = x - startX;

    x += speed;

    if (x > 1920 * 4 || x < 0) {
        speed *= -1;
    }

    if (localX >= 0 && localX <= width) {
         stroke(255, 0, 150);
        strokeWeight(8);
    line(localX, height / 2, localX + 40, height / 2);
    }
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```

### page3
```js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight

}

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point3 = [currentPageData.width / 2, currentPageData.height / 2];
let socket = io('http://localhost:3000')
let speed=5;
let x= 0;

socket.on('connect', () => {
    console.log(socket.id);
    socket.emit('win3update', currentPageData, socket.id);
});

socket.on('getdata', (dataWindow) => {
    remotePageData = dataWindow;
    console.log(remotePageData);
});


let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};


function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
}


function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {
        console.log("Page 3 detected change, sending update:", currentPageData); 
        point2 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win2update', currentPageData, socket.id);
        previousPageData = currentPageData; 
    }
}


function draw() {
  checkWindowPosition();
    background(0);
    let y = height / 2;
    let startX = currentPageData.x;
    let localX = x - startX;

    x += speed;

    if (x > 1920 * 4 || x < 0) {
        speed *= -1;
    }

    if (localX >= 0 && localX <= width) {
         stroke(255, 0, 150);
        strokeWeight(8);
    line(localX, height / 2, localX + 40, height / 2);
}
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```

### page4
```js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight

}

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point4 = [currentPageData.width / 2, currentPageData.height / 2];
let socket = io('http://localhost:3000')
let speed=5;
let x= 0;

socket.on('connect', () => {
    console.log(socket.id);
    socket.emit('win4update', currentPageData, socket.id);
});

socket.on('getdata', (dataWindow) => {
    remotePageData = dataWindow;
    console.log(remotePageData);
});


let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};


function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
}


function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {
        console.log("Page 4 detected change, sending update:", currentPageData); 
        point2 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win4update', currentPageData, socket.id);
        previousPageData = currentPageData; 
    }
}


function draw() {
  checkWindowPosition();
    background(0);
    let y = height / 2;
    let startX = currentPageData.x;
    let localX = x - startX;

    x += speed;

    if (x > 1920 * 4 || x < 0) {
        speed *= -1;
    }

    if (localX >= 0 && localX <= width) {
         stroke(255, 0, 150);
        strokeWeight(8);
    line(localX, height / 2, localX + 40, height / 2);
    }
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```

-----------------------------------------------------------------------------------------------------------------------------

### retos
No me funcionó que la linea pasara a las otras paginas, que esa era mi idea, que se moviera por todas las pages y que rebotara y se devolvira al final.

Otro reto fue que no sabia como hacer con la velocidad, pero al parecer js de una la agarró, debe ser que ese nombre de speed ya esta reservado.

Si fue bastante dificil.

### video

https://youtu.be/g0RDfpNx-cc
