# Internet Explorer

Pokud se v dnešní době z nějakého důvodu nechce věnovat čas do optimalizace stránek pro zastaralý Internet Explorer, jsou dvě možnosti:

1) Přesměrování
2) Varovná hláška


## Přesměrování
Internet Explorer provádí přesměrování do Edge sám na základě seznamu nekompatibilních webů, který spravuje Microsoft.

* https://docs.microsoft.com/en-us/deployedge/edge-learnmore-neededge
* https://docs.microsoft.com/en-us/microsoft-edge/web-platform/ie-to-microsoft-edge-redirection#request-an-update-to-the-ie-compatibility-list

Podobného výsledku lze dosáhnout pomocí JS
```html
<script>
  if(/MSIE \d|Trident.*rv:/.test(navigator.userAgent)) {
    window.location = 'microsoft-edge:' + window.location;
    setTimeout(function() {
      window.location = 'https://go.microsoft.com/fwlink/?linkid=2135547';
    }, 1);
  }
</script>
```
Odkazy na stránky Microsoftu s informacemi o přesměrování.
* [Doporučujeme zobrazit tento web v Microsoft Edge](https://go.microsoft.com/fwlink/?linkid=2151617)
* [Web, na který se snažíte přejít, nefunguje v Internet Exploreru](https://go.microsoft.com/fwlink/?linkid=2135547)

## Varovná hláška

```HTML
<script>
function isIE() {
  ua = navigator.userAgent;
  var is_ie = ua.indexOf("MSIE ") > -1 || ua.indexOf("Trident/") > -1;
  return is_ie;
}
if (isIE() && document.cookie.indexOf('IE') == -1 ){
	alert('Pravděpodobně využíváte Internet Explorer, nebo jiný prohlížeč, využívající jádro Trident. Tento prohlížeč, není nadále vyvýjen již od roku 2013. Sránky se vám tedy nemohou zobrazovat správně!\n\n V případě problémů se zobrazením, změňte internetový prohlížeč.');
	document.cookie = "IE=Nezobrazovat upozornění na Internet Explorer do zavření prohlížeče";
}
</script>
```




## Noscript 
Někdo může mít JavaScript i vypnutý a v takovém případě bude fungovat pouze MS řešení přes compatibility list. 

Upozornění na vypnutý JavaScript.

```html
<noscript>
	<div style="text-align: center; display: block; color: red; font-size: 2rem; background: white; padding: 32px;">
	<p><strong>Zdá se, že&nbsp;Váš prohlížeč nepodporuje Javascript!</strong></p>
	<p>Otevřete stránky v&nbsp;jiném prohlížeči nebo <a target="_blank" rel="nofollow noreferrer noopener" href="https://www.google.com/search?q=jak+povolit+javascript" style="color: red">povolte&nbsp;JavasScript</a>, aby&nbsp;se&nbsp;stránky načetli v&nbsp;pořádku.</p>
	</div>
</noscript>
```

Nevýhoda JS řešení oproti Microsoft žádosti je to, že uživatel bude přesměrován i tehdy, když má IE ale zároveň nemá Edge.
Na druhou stranu Edge byl zpětně doinstalován i do starých Win7. Takže uživatelů používajících IE, kteří nemají Edge by mělo být v dnešní době minimum.
