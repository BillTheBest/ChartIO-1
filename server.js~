var app = require('express')()
, server = require('http').createServer(app)
, io = require('socket.io').listen(server);

//Inciando server na porta 3000, utilizando uma função de callback
//para indicar o inicio do servidor
server.listen(3000, function(){
   console.log("Iniciando...");
});

io.configure('development', function(){
  io.set('log level', 1);
});

//Adcionando uma rota com o framework express
app.get('/', function(req, res){
	res.sendfile(__dirname + '/chart.html');
});

app.get('/js/highcharts.js', function(req, res){
	res.sendfile(__dirname + '/highcharts.js')
});

app.get('/js/gray.js', function(req, res){
	res.sendfile(__dirname + '/gray.js')
});

var votos = [0,0];

//Eventos do socket
io.sockets.on('connection', function(socket){

	socket.on('enviarVoto', function(data){
		votos[data.voto] += 1;
		console.log(votos[data.voto]);
		socket.emit('receberVoto', data.voto);
		socket.broadcast.emit('receberVoto', data.voto);
	});


	socket.on('receberVotos', function(){
		console.log('aqui'+ votos);
		socket.emit('enviarVotacao', votos);
	})

});