# Ćwiczenia z XML-RPC
Plik z zadaniami z zajęć z XML-RPC


# Wstęp

Do rozwiązania poniższych zadań wykorzystamy język Java, pakiet org.apache.xmlrpc będący implementacją protokołu XML-RPC oraz narzędzie Maven. Zalecanym środowiskiem wykonywania zadań jest IntelliJ IDEA. W celu przetestowania implementacji serwera przydatny będzie również program Postman.

# Zadania
1. Na początek zaimplementujemy prosty serwer. Uruchom proszę IntelliJ IDEA i utwórz nowy projekt. Jako typ projektu wybierz Maven.
2. Zaimportuj bibliotekę org.apache.xmlrcp za pomocą Mavena. W tym celu otwórz plik pom.xml i sekcji w sekcji dependiences wklej następujący kod. 
```xml
<!-- https://mvnrepository.com/artifact/org.apache.xmlrpc/xmlrpc -->
<dependency>
    <groupId>org.apache.xmlrpc</groupId>
    <artifactId>xmlrpc</artifactId>
    <version>3.1.3</version>
    <type>pom</type>
</dependency>
```
Uwaga! Jeśli Maven nie wygenerował sekcji dependiences utwórz ją wpisując ```<dependiences></dependiences>```
3. Zapoznaj się z poniższym kodem i skopuj metodę *Main* do swojej klasy
```Java
public static void main (String [] args){
        try {
            // Uruchomienie serwera HTTP na porcie 80
            // Ten serwer obsługuje tylko żądania XML-RPC
            WebServer webServer = new WebServer(80);
            XmlRpcServer xmlRpcServer = webServer.getXmlRpcServer();

            // Konfiguracja uchwytów do klas implementujących metody, które
            // chcemy wystawić naszym klientom.
            PropertyHandlerMapping phm = new PropertyHandlerMapping();
            // Pierwszy argument to nazwa, której użyjemy do identyfikowania danej klasy
            // Drugi argument to klasa, której metody publiczne chcemy udostępnić
            phm.addHandler("hello", JavaServer.class);

            // Po ustawieniu wszystkich uchwytów możemy przypisać mapowanie do serwera
            xmlRpcServer.setHandlerMapping(phm);
            // uruchomienie serwera
            webServer.start();

            System.out.println("Serwer pracuje...");

        } catch (Exception exception){
            System.err.println("Nie można uruchomić serwera: " + exception);
        }//catch()
    }//main()
```
4. Zaimplementuj teraz w tej samej klasie metodę sayHello, która nie przyjmuje żadnych parametrów i zwraca *String*. Możesz w niej zwrócić dowolny napis witający użytkownika.
5. Uruchom program. Na konsoli powinien zostanać wyświetlony napis 
> Serwer pracuje...
