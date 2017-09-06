#include <stdio.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <string.h>
#include <stdlib.h>

int main(){

 int SocketCreate, NewSocket;
 char msg[1024];
 struct sockaddr_in ServerAddr;
 struct sockaddr_storage ServerStorage;
 socklen_t AddrSize;

 //Creating socket - Tworzenie gniazda
 SocketCreate = socket(PF_INET, SOCK_STREAM,0);
  if(SocketCreate<0){
	printf("Socket Create error\n"); //Socket error - Blad tworzenia gniazda
	exit(1);
  }

 //Configuration settings of the adress - konfiguracja ustawien adresow
 ServerAddr.sin_family = AF_INET;
 ServerAddr.sin_port = htons(8888); //port number - numer portu
 ServerAddr.sin_addr.s_addr = htonl(INADDR_ANY); //Ip to localhost - ustawienie ip

 //set padding bits to 0 - wyzerowanie pola bitow wypełnienia(cokolwiek to znaczy)
 memset(ServerAddr.sin_zero, '\0',sizeof ServerAddr.sin_zero);

 //Bind socket to adress - Wiązanie gniazda z adresem
 bind(SocketCreate, (struct sockaddr *) &ServerAddr, sizeof(ServerAddr));
  /*if(bind(SocketCreate, (struct sockaddr *) &ServerAddr, sizeof(ServerAddr))<0){
	printf("Bind error\n"); //Bind error - Blad przy wiazaniu 
	exit(1);
 }*/

 //Listen on the socket - nasłuchiwanie socketa
 listen(SocketCreate,5);
  if(listen(SocketCreate,5)==0)
	printf("Nasluchiwanie..\n");
  else
	printf("Blad przy nasluchiwaniu\n"); 
  

 //Accept call creates scket for connection-start socketa akceptujacego polaczenie
 AddrSize = sizeof ServerStorage; //adres klienta
 NewSocket = accept(SocketCreate, (struct sockaddr *) &ServerStorage, &AddrSize);
  if(NewSocket<0){
	printf("Socket error"); //Socket error - Blad przy tworzeniu gniazda
        exit(1);
  }
 //Send message to the socket - wyslanie wiadomosci do gniazda
  for(;;){

  recv(NewSocket,msg,1024,0);
  printf("Klient:%s",msg);
  bzero(msg,1024); 

/*WYSYLANIE ******************************
  bzero(msg,1024);
  printf("Serwer:");
  fgets(msg,1024,stdin);
  send(NewSocket,msg,strlen(msg),0);
******************************************/
/*ODBIERANIE ******************************
  recv(NewSocket,msg,1024,0);
  printf("Klient:%s",msg);
  bzero(msg,1024); 
******************************************/
  }
 //close(NewSocket);
 //close(SocketCreate);
 return 0;
}

