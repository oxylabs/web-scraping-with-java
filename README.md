# web-scraping-with-java
Web Scraping With Java


```java
<dependencies>
    <dependency>
        <groupId>org.jsoup</groupId>
        <artifactId>jsoup</artifactId>
        <version>1.14.1</version>
    </dependency>
</dependencies>
```

```java
import org.jsoup.Connection;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
```

```java
Document doc = Jsoup.connect("https://en.wikipedia.org/wiki/Jsoup").get();
```

```java
public static Document getDocument(String url) {
    Connection conn = Jsoup.connect(url);
    Document document = null;
    try {
        document = conn.get();
    } catch (IOException e) {
        e.printStackTrace();
    // handle error
    }
    return document;
}
```

```java
Connection conn = Jsoup.connect(url);
conn.userAgent("custom user agent");
document = conn.get();
```

```java
Element firstHeading = document.getElementsByClass("firstHeading").first();
System.out.println(firstHeading.text());
```

```java
Element firstHeading= document.selectFirst(".firstHeading"); 
```

```java
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.51.0</version>
</dependency>
```

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.DomNode;
import com.gargoylesoftware.htmlunit.html.DomNodeList;
import com.gargoylesoftware.htmlunit.html.HtmlElement;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
```

```java
WebClient webClient = new WebClient();
webClient.getOptions().setCssEnabled(false);
webClient.getOptions().setJavaScriptEnabled(false);
HtmlPage page = webClient.getPage("https://librivox.org/the-first-men-in-the-moon-by-hg-wells");
```

```java
public static HtmlPage getDocument(String url) {
    HtmlPage page = null;
    try (final WebClient webClient = new WebClient()) {
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(false);
        page = webClient.getPage(url);
    } catch (IOException e) {
        e.printStackTrace();
    }
    return page;
} 
```

```java
HtmlPage page = webClient.getPage("https://en.wikipedia.org/wiki/Jsoup");
DomElement firstHeading = page.getElementById("firstHeading");
System.out.print(firstHeading.asNormalizedText()); // prints Jsoup
```

```java
HtmlElement book = page.getFirstByXPath("//div[@class=\"content-wrap clearfix\"]/h1");
System.out.print(book.asNormalizedText());
```

```java
String selector = ".chapter-download tbody tr";
DomNodeList<DomNode> rows = page.querySelectorAll(selector);
for (DomNode row : rows) {
    String chapter = row.querySelector("td:nth-child(2) a").asNormalizedText();
    String reader = row.querySelector("td:nth-child(3) a").asNormalizedText();
    String duration = row.querySelector("td:nth-child(4)").asNormalizedText();
    System.out.println(chapter + "\t " + reader + "\t " + duration);
}
```
