/\*\*

`* ProveIt is a powerful reference manager for Wikipedia`
`* Documentation at `<https://commons.wikimedia.org/wiki/Help:Gadget-ProveIt>
`*`
`* This script sets the configuration options specific to this wiki`
`* and loads the gadget code from Wikimedia Commons`
`*/`

function loadProveIt() {

`   mw.config.set({`
`       'proveit-tag': 'ProveIt edit', // Revision tag defined at Special:Tags (optional)`
`       'proveit-summary': 'Reference edited with `[`ProveIt`](https://zh.wikipedia.org/wiki/Commons:Help:Gadget-ProveIt "wikilink")`', // Automatic edit summary (optional)`
`       'proveit-templates': [ // Citation templates (without namespace)`
`           'Citation',`
`           'Cite arXiv',`
`           'Cite AV media',`
`           'Cite book',`
`           'Cite bioRxiv',`
`           'Cite comic',`
`           'Cite encyclopedia',`
`           'Cite episode',`
`           'Cite interview',`
`           'Cite journal',`
`           'Cite magazine',`
`           'Cite news',`
`           'Cite paper',`
`           'Cite press release',`
`           'Cite report',`
`           'Cite sign',`
`           'Cite speech',`
`           'Cite thesis',`
`           'Cite tweet',`
`           'Cite video',`
`           'Cite video game',`
`           'Cite web',`
`       ],`
`       'proveit-namespaces': [ // Supported namespaces (see `<https://www.mediawiki.org/wiki/Manual:Namespace_constants>`)`
`           0, // Main namespace`
`           2, // User namespace`
`       ]`
`   });`
`   mw.loader.load( '//commons.wikimedia.org/w/load.php?modules=ext.gadget.ProveIt&only=scripts' );`
`   mw.loader.load( '//commons.wikimedia.org/w/load.php?modules=ext.gadget.ProveIt&only=styles', 'text/css' );`

}

// Only load when editing mw.hook( 'wikipage.editform' ).add( loadProveIt ); mw.hook( 've.activationComplete' ).add( loadProveIt );