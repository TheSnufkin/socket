
1. send(NewSocket,bufor,strlen(bufor),0); - wyslanie wiadomosci string gniazdem
   recv(ClientSocket,bufor,1024,0);       - odbieranie wiadomosci string z gniazda
   
   write(ClientSocket,&num,sizeof(num));  - wyslanie wiadomosci int gniazdem
   read(NewSocket,&num,sizeof(num));      - odbieranie wiadomosci int z gniazda
  *ew do wysyłania int konwersja zmiennej lokalna/sieciowa: htonl()(do wysylania) i ntohl()(odb)

2. atoi() - konwersja z char na int
   Przykład: int numer = atoi(napis);

3. sprintf(tab, "%d", a); -  wklejanie inta do chara
 
4. bzero(Char,długosc) - zerowanie tablicy char. 
   Przykład: bzero(Tablica,1024);

5. strcpy(Gdzie, kopiowane) - wklejanie/wpisywanie stringa
   Przykład: strcpy(Tablica,"to bedzie tablica\n"); / strcpy(Tablica,Tablica2);

6. fgets(gdzie,dlugosc tab,stdin); - input z klawiatury do chara 
   Przykład: fgets(wiadomosc,200,stdin);

7. scanf("%d",&num); - pobieranie inta z inputa


8. htonl(INADDR_ANY); - w " adres_servera.sin_addr.s_addr = htonl(INADDR_ANY);" 
   -"zamiast inet_addr("127.16.0.100");" przy konfigurowaniu struktur adresow w serwerze ip na localhosta







1. poradnik do podstawy: http://www.programminglogic.com/example-of-client-server-program-in-c-using-sockets-and-tcp/

2. chyba ładnie wytlumaczone: http://www.thegeekstuff.com/2011/12/c-socket-programming/?utm_source=feedburner

4.https://github.com/bschmaltz/c-p2p-chat - p2p

5. http://beej.us/guide/bgnet/output/html/singlepage/bgnet.html - ponoc dobre

6. http://www.cs.rpi.edu/~moorthy/Courses/os98/Pgms/socket.html - sockety
