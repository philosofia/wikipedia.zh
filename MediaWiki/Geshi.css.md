> 本文内容由[MediaWiki:Geshi.css](https://zh.wikipedia.org/wiki/MediaWiki:Geshi.css)转换而来。


/\*

``` css
 */

/* This css will override styles used by the GeSHi syntax highlighting,
   such that less awful colors for the highlighting can be chosen. */


/**
 * Language code: "vb"
 *
 * Overrides colors used for keywords from that horrible gold
 * to more tolerable blue. Other colors left as default at present time.
 */
.source-vb .kw1 {color: #006 !important }


/**
 * Language code: "cpp"
 *
 * Color fix for member variables
 */
.source-cpp .me1 { color:#499; }
.source-cpp .me2 { color:#499; }


/* Reinstating borders */

body.skin-monobook div.mw-geshi {
  padding: 1em;
  border: 1px dashed #2f6fab;
  color: black;
  background-color: #f9f9f9;
  line-height: 1.1em;
}

body.skin-modern div.mw-geshi {
  border: solid 1px #3c78b5;
  padding: 0.4em;
  background-color: #f0f0f0;
}

body.skin-simple div.mw-geshi {
  margin: 2em;
  border: solid 1px black;
}

body.skin-chick div.mw-geshi {
  padding: 1em;
  border: 1px dashed #2f6fab;
  color: black;
  background-color: #f9f9f9;
  line-height: 1.1em;
}

body.skin-vector div.mw-geshi {
  padding: 1em;
  border: 1px dashed #2f6fab;
  color: black;
  background-color: #f9f9f9;
  line-height: 1.1em;
}


/*
```

\*/