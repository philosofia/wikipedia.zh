var MainPageCustomization = {};

MainPageCustomization.set = function(p) {

`   if (MainPageCustomization.pageName == undefined) {`
`       MainPageCustomization.pageName = p;`
`   } else {`
`       MainPageCustomization.pageName = null;`
`       alert('You chose more than one main page style.');`
`       window.location.href = mw.config.get('wgScript') + '?title=Special:Preferences#prefsection-8';`
`   }`

};

$(function() {

`   if (mw.config.get('wgIsMainPage')) {`
`       if ((mw.config.get('wgAction') == 'view' || mw.config.get('wgAction') == 'purge') && MainPageCustomization.pageName) {`
`           // #article is for some old skins`
`           jQuery('.mw-content-ltr').text('Loading customized main page...').show().load(mw.config.get('wgScript'), {`
`               action: 'render',`
`               title: MainPageCustomization.pageName`
`           }, function(response, status, xhr) {`
`               if (status == 'error') {`
`                   jQuery('.mw-content-ltr').text('Sorry, but there was an error when '`
`                       + 'loading customized main page: ' + xhr.status + ' ' + xhr.statusText`
`                   );`
`               }`
`           });`
`       } else {`
`           jQuery('.mw-content-ltr').show();`
`       }`
`   }`

});