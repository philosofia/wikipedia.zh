/\*\*

`* Metadata assessment script`
`* Finds the WP 1.0/WikiProject assessment of every article you go to, then`
`* displays that information in the article header.`
`* @author Outriggr - created the script and used to maintain it`
`* @author Pyrospirit - currently maintains and updates the script`

from [:en:MediaWiki:Gadget-metadata.js](https://zh.wikipedia.org/wiki/:en:MediaWiki:Gadget-metadata.js "wikilink")

`*/`

// Import stylesheet with custom classes for header colors importStylesheet('User:Shizhao/metadata.css');

var assessment = {

`   autorun: true,`
`   showOldPeerReviews: false,`
`   /**`
`    * Starts the script object running. The main function of the script. If the`
`    * getMainType() function can find the assessment, it uses that assessment`
`    * for the page, parses it, and displays it in the header. Otherwise, it runs`
`    * ajaxMain().`
`    */`
`   init: function init () {`
`       this.callHooks('init_before');`
`       var initialAssessment = this.checkArticle(); // checks for types visible from article page`
`       if (initialAssessment.exists) {`
`           this.currentAssessment = initialAssessment;`
`           var data = this.talkAssess(this.currentAssessment);`
`           this.update(data.newClass, data.slogan, data.info);`
`       }`
`       else this.ajaxMain(); // proceed to check the talk page`
`       this.callHooks('init_after');`
`   },`
`   /**`
`    * The main function when an AJAX request is needed to find the assessment.`
`    * Creates an AJAX request for the contents of a URL (defaults to the`
`    * first section of the article's talk page), then sends the request. After`
`    * getting the requested data back, it finds the assessment information in`
`    * the data, then uses and displays that assessment in the header.`
`    * @param {String} url - Optional: override the default URL for the request.`
`    * @param {Function} stateChange - Optional: override the default request callback`
`    * @param optionalArgument - Optional: passed to the stateChange function`
`    */`
`   ajaxMain: function ajaxMain (url, stateChange, optionalArgument) {`
`       if (!url || !/^https?:\/\//i.test(url)) // optional url override`
`           url = mw.config.get('wgServer') + mw.config.get('wgScript') + '?title=Talk:' + encodeURIComponent(mw.config.get('wgPageName'))`
`           + '&action=raw&section=0';`
`       if (typeof stateChange !== 'function') {`
`           stateChange = this.stateChange;`
`           this.url = url;`
`       }`
`       var request = sajax_init_object();`
`       if (request) {`
`           var that = this; // store value of 'this'`
`           request.onreadystatechange = function () {`
`               stateChange.call(that, request, optionalArgument);`
`           }`
`           request.open('GET', url, true);`
`           request.send(null);`
`       }`
`   },`
`   /**`
`    * This function is passed as a parameter to ajaxMain. It is called each time`
`    * this.request updates, and the code inside the conditional runs when the`
`    * data is available.`
`    */`
`   stateChange: function stateChange (request) {`
`       if (request.readyState == 4 && request.status == 200) {`
`           this.text = request.responseText;`
`           this.request = request;`
`           var rating = this.getRating(this.text);`
`           this.currentAssessment = this.getAssessment(this.text, rating);`
`           var data = this.talkAssess(this.currentAssessment);`
`           this.update(data.newClass, data.slogan, data.info);`
`           this.callHooks('onCompletedRequest');`
`       }`
`   },`
`   /**`
`    * Checks for various objects on the article page that indicate a certain`
`    * assessment, such as a featured star or disambiguation page notice. If this`
`    * function can find the assessment, AJAX is not needed for this page.`
`    * @return {Object} assess - the assessment in an easily readable format`
`    * @static`
`    */`
`   checkArticle: function checkArticle () {`
`       var assess = {};`
`       assess.extra == '';`
`       assess.exists = true;`
`       if (document.getElementById('disambig') || document.getElementById('disambig_disambigbox')`
`               || document.getElementById('disambigbox'))`
`           assess.rating = 'dab';`
`       else if (document.getElementById('setindexbox'))`
`           assess.rating = 'setindex';`
`       else if (document.getElementById('contentSub')`
`               && document.getElementById('contentSub').innerHTML == 'Redirect page')`
`           assess.rating = 'redir';`
`       else if (document.getElementById('ca-talk')`
`               && document.getElementById('ca-talk').className == 'new') // no talk page`
`           assess.rating = 'none';`
`       else assess.exists = false; // none of the above, no assessment found`
`       return assess;`
`   },`
`   /**`
`    * Searches the provided wikicode for the rating part of an assessment and`
`    * returns it as a string.`
`    * Note that a higher assessment takes priority, and less-used assessments`
`    * such as "list", "current", or "future" are used only if nothing else can`
`    * be found.`
`    * @param {String} text - some wikitext to be searched for assessment info`
`    * @return {String} rating - the article's current assessment`
`    */`
`   getRating: function getRating (text) {`
`       this.callHooks('getRating_before');`
`       var rating = 'none';`
`       if (text.match(/\|\s*(class|currentstatus)\s*=\s*fa\b/i))`
`           rating = 'fa';`
`       else if (text.match(/\|\s*(class|currentstatus)\s*=\s*fl\b/i))`
`           rating = 'fl';`
`       else if (text.match(/\|\s*class\s*=\s*a\b/i)) {`
`           if (text.match(/\|\s*class\s*=\s*ga\b|\|\s*currentstatus\s*=\s*(ffa\/)?ga\b/i))`
`               rating = 'a/ga'; // A-class articles that are also GA's`
`           else rating = 'a';`
`       } else if (text.match(/\|\s*class\s*=\s*ga\b|\|\s*currentstatus\s*=\s*(ffa\/)?ga\b|\{\{\s*ga\s*\|/i)`
`                  && !text.match(/\|\s*currentstatus\s*=\s*dga\b/i))`
`           rating = 'ga';`
`       else if (text.match(/\|\s*class\s*=\s*b\b/i))`
`           rating = 'b';`
`       else if (text.match(/\|\s*class\s*=\s*bplus\b/i))`
`           rating = 'bplus'; // used by WP Math`
`       else if (text.match(/\|\s*class\s*=\s*c\b/i))`
`           rating = 'c';`
`       else if (text.match(/\|\s*class\s*=\s*start/i))`
`           rating = 'start';`
`       else if (text.match(/\|\s*class\s*=\s*stub/i))`
`           rating = 'stub';`
`       else if (text.match(/\|\s*class\s*=\s*list/i))`
`           rating = 'list';`
`       else if (text.match(/\|\s*class\s*=\s*sl/i))`
`           rating = 'sl'; // used by WP Plants`
`       else if (text.match(/\|\s*class\s*=\s*(dab|disambig)/i))`
`           rating = 'dab';`
`       else if (text.match(/\|\s*class\s*=\s*cur(rent)?/i))`
`           rating = 'cur';`
`       else if (text.match(/\|\s*class\s*=\s*future/i))`
`           rating = 'future';`
`       this.callHooks('getRating_after');`
`       return rating;`
`   },`
`   /**`
`    * Searches the provided wikicode for data on the article's current and past`
`    * featured or good status and returns an object that contains this data`
`    * along with some miscellaneous other bits of information.`
`    * @param {String} text - some wikitext to be searched for assessment info`
`    * @return {Object} assess - the assessment data for the page`
`    */`
`   getAssessment: function getAssessment (text, rating) {`
`       this.callHooks('getAssessment_before');`
`       var assess = {rating: rating, pageLink: [null, null], extra: [], activeReview: null};`
`       var actionNumber = 0, pageLinkFlag = false, tempMatch, articleName;`

`       // Current nominations (FAC, FLC, or GAN)`
`       if ((assess.reg = text.match(/\{\{\s*FAC\s*(?:[\|\}]\s*([^\|\}]*))?[^\}]*?\}\}/i))) {`
`           assess.extra.push('fac');`
`           if (assess.reg[1] && (articleName = this.decodeEntities(assess.reg[1].trim())))`
`               assess.pageLink[0] = 'Wikipedia:特色条目评选\/' + articleName;`
`       } else if ((assess.reg = text.match(/\{\{\s*FLC\s*(?:[\|\}]\s*([^\|\}]*))?[^\}]*?\}\}/i))) {`
`           assess.extra.push('flc');`
`           if (assess.reg[1] && (articleName = this.decodeEntities(assess.reg[1].trim())))`
`               assess.pageLink[0] = 'Wikipedia:特色列表评选\/' + articleName;`
`       } else if ((assess.reg = text.match(/\{\{\s*GAnominee\s*[\|\}][^\}]*\}\}/i))) {`
`           assess.extra.push('gan');`
`           if (assess.reg[1] && (articleName = this.decodeEntities(assess.reg[1].trim())))`
`               assess.pageLink[0] = 'Wikipedia:優良條目候選\#' + articleName;`
`       }`
`       // Current reviews of a status (FAR, FLRC, or GAR)`
`       else if ((assess.reg = text.match(/\{\{\s*FAR\s*(?:[\|\}]\s*([^\|\}]*))?[^\}]*?\}\}/i))) {`
`           assess.extra.push('far');`
`           if (assess.reg[1] && (articleName = this.decodeEntities(assess.reg[1].trim())))`
`               assess.pageLink[0] = 'Wikipedia:特色列表评选\/' + articleName;`
`       } else if ((assess.reg = text.match(/\{\{\s*featured[ _]list[ _]removal[ _]candidates\s*(?:[\|\}]\s*([^\|\}]*))?[^\}]*?\}\}/i))) {`
`           assess.extra.push('flrc');`
`           if (assess.reg[1] && (articleName = this.decodeEntities(assess.reg[1].trim())))`
`               assess.pageLink[0] = 'Wikiprdia:特色列表评选\/' + articleName;`
`       } else if ((assess.reg = text.match(/\{\{\s*GArevoke\s*[\|\}][^\}]*\}\}/i))) {`
`           assess.extra.push('gar');`
`           if (assess.reg[1] && (articleName = this.decodeEntities(assess.reg[1].trim())))`
`               assess.pageLink[0] = 'Wikipedia:優良條目重審\#' + articleName;`
`       }`
`       // Former statuses (FFA, FFL, or DGA)`
`       if ((assess.reg = text.match(/\|\s*currentstatus\s*=\s*ffa\b/i))) {`
`           tempMatch = text.match(/\|\s*action(\d+)\s*=\s*far\b/gi);`
`           actionNumber = tempMatch[tempMatch.length - 1].match(/\d+/);`
`           pageLinkFlag = true;`
`           assess.extra.push('ffa');`
`       } else if ((assess.reg = text.match(/\|\s*action(\d+)\s*=\s*far\b/gi))`
`               // This checks if the last FAR entry in ArticleHistory resulted in removal.`
`               && text.match(RegExp(`
`                   '\\|\\s*action' + assess.reg[assess.reg.length - 1].match(/\d+/)`
`                       + 'result\\s*=\\s*removed\\b', 'i'`
`               )) && assess.rating.search(/f[al]/i) == -1) {`
`           actionNumber = assess.reg[assess.reg.length - 1].match(/\d+/);`
`           pageLinkFlag = true;`
`           assess.extra.push('ffa');`
`       } else if ((assess.reg = text.match(/\{\{\s*formerfa2?\b/i))) {`
`           assess.extra.push('ffa');`
`       } else if ((assess.reg = text.match(/\|\s*currentstatus\s*=\s*ffl\b/i))) {`
`           assess.extra.push('ffl');`
`       } else if ((assess.reg = text.match(/\{\{\s*ffl\s*[\|\}]/i))) {`
`           assess.extra.push('ffl');`
`       } else if ((assess.reg = text.match(/\|\s*currentstatus\s*=\s*dga\b/i))) {`
`           tempMatch = text.match(/\|\s*action(\d+)\s*=\s*gar\b/gi);`
`           actionNumber = tempMatch[tempMatch.length - 1].match(/\d+/);`
`           pageLinkFlag = true;`
`           assess.extra.push('dga');`
`       } else if ((assess.reg = text.match(/\{\{\s*d(elisted)?ga\s*[\|\}]/i))) {`
`           assess.extra.push('dga');`
`       }`
`       // Former nominations (former FAC, FLC, or GAN)`
`       else if ((assess.reg = text.match(/\|\s*action(\d+)\s*=\s*fac\b/gi))`
`               && assess.rating.search(/f[al]/i) == -1) {`
`           actionNumber = assess.reg[assess.reg.length - 1].match(/\d+/);`
`           pageLinkFlag = true;`
`           assess.extra.push('ffac');`
`       } else if ((assess.reg = text.match(/\|\s*currentstatus\s*=\s*ffac\b/i))) {`
`           assess.extra.push('ffac');`
`       } else if ((assess.reg = text.match(/\{\{\s*fac?(failed|(\-|[ _]`\()?contested\)`?)\s*[\|\}]/i))) {`
`           assess.extra.push('ffac');`
`       } else if ((assess.reg = text.match(/\|\s*action(\d+)\s*=\s*flc\b/gi))`
`               && assess.rating.search(/f[al]/i) == -1) {`
`           actionNumber = assess.reg[assess.reg.length - 1].match(/\d+/);`
`           pageLinkFlag = true;`
`           assess.extra.push('fflc');`
`       } else if ((assess.reg = text.match(/\|\s*currentstatus\s*=\s*fflc\b/i))) {`
`           assess.extra.push('fflc');`
`       } else if ((assess.reg = text.match(/\|\s*action(\d+)\s*=\s*gan\b/gi))`
`               && assess.rating.search(/f[al]|(a\/)?ga/i) == -1) {`
`           actionNumber = assess.reg[assess.reg.length - 1].match(/\d+/);`
`           pageLinkFlag = true;`
`           assess.extra.push('fgan');`
`       } else if ((assess.reg = text.match(/\|\s*currentstatus\s*=\s*fgan\b/i))) {`
`           assess.extra.push('fgan');`
`       } else if ((assess.reg = text.match(/\{\{\s*f(ailed ?)?ga\s*[\|\}]/i))) {`
`           assess.extra.push('fgan');`
`       }`

`       // Looks for currently active peer reviews`
`       var peerReview;`
`       if ((peerReview = text.match(/\{\{\s*Peerreview\s*\|\s*archive\s*=\s*(\d+)\b/i))) {`
`           assess.review = 'Wikipedia:同行评审/' + mw.config.get('wgPageName')`
`               + peerReview[1];`
`           assess.activeReview = true;`
`       } else if (this.showOldPeerReviews) {`
`           // TODO: Add code for old peer reviews`
`       } else assess.review = null;`

`       // Scans for the link associated with an action in ArticleHistory`
`       if (pageLinkFlag) {`
`           var linkPattern = RegExp('\\|\\s*action' + actionNumber + 'link\\s*=\\s*([^\\n\\|]+)\\s*\\|');`
`           var linkMatch = text.match(linkPattern);`
`           assess.pageLink[1] = linkMatch ? this.decodeEntities(linkMatch[1]) : null;`
`       }`

`       assess.exists = true;`
`       this.callHooks('getAssessment_after');`
`       return assess;`
`   },`
`   /**`
`    * Parses an assessment object into the HTML and CSS code needed to update`
`    * the article header. If it doesn't recognize a part of the information`
`    * given, it will simply ignore it and mark as unassessed.`
`    * @param {Object} assess - assessment information for this article`
`    * @return {String} newClass - the CSS class corresponding to its assessment`
`    * @return {String} slogan - HTML giving (with a link) the main assessment`
`    * @return {String} info - HTML giving (with a link) additional information`
`    */`
`   talkAssess: function talkAssess (assess) {`
`       this.callHooks('talkAssess_before');`

`       var path = mw.config.get('wgArticlePath').replace('$1', '');`
`       var assessLink = path + 'Wikipedia:专题委员会/评级问答';`
`       if (typeof assess.extra === 'undefined') assess.extra = '';`
`       var extra = assess.extra, rating = assess.rating;`
`       var pageLink = assess.pageLink ? [this.encodePageName(assess.pageLink[0]),`
`           this.encodePageName(assess.pageLink[1])] : [null, null];`
`       var peerReview = this.encodePageName(assess.review);`

`       var info = this.getExtraInfo(extra, pageLink);`
`       var peerReviewText = this.addPeerReview(peerReview, assess.activeReview);`
`       if (peerReviewText)`
`           info.push(peerReviewText);`
`       var newClass, slogan;`

`       if (rating == 'a' || rating == 'a/ga') {`
`           newClass = 'assess-a-text';`
`           slogan = '`<a href="' + assessLink + '">`甲级`</a>`条目';`
`           if (rating == 'a/ga') {`
`               info.push('也是`<a href="' + path + 'Wikipedia:優良條目">`优良条目`</a>`.');`
`           }`
`       } else if (rating == 'ga') {`
`           newClass = 'assess-ga-text';`
`           slogan = '`<a href="' + path + 'Wikipedia:優良條目">`优良条目`</a>`'`
`       } else if (rating == 'b') {`
`           newClass = 'assess-b-text';`
`           slogan = '`<a href="' + assessLink + '">`乙级`</a>`条目';`
`       } else if (rating == 'bplus') {`
`           newClass = 'assess-bplus-text';`
`           slogan = 'A `<a href="' + path + 'Wikipedia:WikiProject_Mathematics/Wikipedia_1.0'
                + '/Grading_scheme">`乙+级`</a>`条目';`
`       } else if (rating == 'c') {`
`           newClass = 'assess-c-text';`
`           slogan = '`<a href="' + assessLink + '">`丙级`</a>`条目';`
`       } else if (rating == 'start') {`
`           newClass = 'assess-start-text';`
`           slogan = '`<a href="' + assessLink + '">`初级`</a>`条目';`
`       } else if (rating == 'stub') {`
`           newClass = 'assess-stub-text';`
`           slogan = '`<a href="' + assessLink + '">`小作品级`</a>`条目';`
`       } else if (rating == 'sl') {`
`           newClass = 'assess-sl-text';`
`           slogan = '`<a href="' + assessLink + '">`小作品级`</a>`列表';`
`       } else if (rating == 'list') {`
`           newClass = 'assess-list-text';`
`           slogan = '`<a href="' + path + 'Wikipedia:列表">`列表级`</a>`条目';`
`       } else if (rating == 'dab') {`
`           newClass = 'assess-dab-text';`
`           slogan = '`<a href="' + path + 'Wikipedia:消歧义">`消歧义页`</a>`';`
`       } else if (rating == 'setindex') {`
`           newClass = 'assess-setindex-text';`
`           slogan = '`<a href="' + path + 'Wikipedia:Disambiguation#Set_index_articles">`'`
`               + 'set index article`</a>`';`
`       } else if (rating == 'redir') {`
`           newClass = 'assess-redir-text';`
`           slogan = '`<a href="' + path + 'Help:重定向">`重定向页`</a>`';`
`       } else if (rating == 'fl') {`
`           newClass = 'assess-fl-text';`
`           slogan = '`<a href="' + path + 'Wikipedia:特色列表">`特色列表`</a>`';`
`       } else if (rating == 'fa') {`
`           newClass = 'assess-fa-text';`
`           slogan = '`<a href="' + path + 'Wikipedia:特色条目">`特色条目`</a>`';`
`       } else if (rating == 'cur') {`
`           newClass = 'assess-cur-text';`
`           slogan = '`<a href="' + path + 'Portal:新闻动态">`新闻动态级`</a>`条目';`
`       } else if (rating == 'future') {`
`           newClass = 'assess-future-text';`
`           slogan = '`<a href="' + path + 'Category:未来级条目">`未来级`</a>`'`
`               + '条目';`
`       } else {`
`           newClass = 'assess-unassessed-text';`
`           slogan = '`<a href="' + assessLink + '">`未评级`</a>`条目';`
`       }`

`       this.callHooks('talkAssess_after');`
`       return {newClass: newClass, slogan: slogan, info: info};`
`   },`
`   /**`
`    * Creates an info string based on the assessment info and a page link.`
`    */`
`   getExtraInfo: function getExtraInfo (extra, pageLink) {`
`       var info = [];`
`       var page = this.encodePageName(mw.config.get('wgPageName'));`
`       // Current nominations and reviews`
`       if (extra.indexOf('fac') != -1) {`
`           info.push(this.makeInfoString('当前正在', pageLink[0], 'Wikipedia:特色条目评选/'`
`               + page, '特色条目评选', null));`
`       } else if (extra.indexOf('flc') != -1) {`
`           info.push(this.makeInfoString('当前正在', pageLink[0], 'Wikipedia:特色列表评选/'`
`               + page, '特色列表评选', null));`
`       } else if (extra.indexOf('gan') != -1) {`
`           info.push(this.makeInfoString('当前正在', pageLink[0], 'Wikipedia:優良條目候選',`
`               '優良條目候選', null));`
`       } else if (extra.indexOf('far') != -1) {`
`           info.push(this.makeInfoString('当前正在', pageLink[0], 'Wikipedia:特色条目评选/'`
`               + page, '特色条目重选'));`
`       } else if (extra.indexOf('flrc') != -1) {`
`           info.push(this.makeInfoString('当前正在', pageLink[0], 'Wikipedia:特色列表评选/'`
`               + page, '特色列表重选', null));`
`       } else if (extra.indexOf('gar') != -1) {`
`           info.push(this.makeInfoString('`<span id="assess-gar-link">`当前正在', pageLink[0],`
`               'Wikipedia:優良條目重審', '優良條目重審', '<\/span>'));`
`       }`
`       // Past statuses and nominations`
`       if (extra.indexOf('ffa') != -1) {`
`           info.push(this.makeInfoString('', pageLink[1], 'Wikipedia:特色條目评选/' + page,`
`               '曾经是', '特色条目'));`
`       } else if (extra.indexOf('ffl') != -1) {`
`           info.push(this.makeInfoString('', pageLink[1], 'Wikipedia:特色列表评选/'`
`               + page, '曾经是', '特色列表'));`
`       } else if (extra.indexOf('dga') != -1) {`
`           info.push(this.makeInfoString('', pageLink[1], 'Wikipedia:優良條目重審',`
`               '曾经是', '优良条目'));`
`       } else if (extra.indexOf('ffac') != -1) {`
`           info.push(this.makeInfoString('曾參與', pageLink[1], 'Wikipedia:特色条目评选/'`
`               + page, '特色条目评选', null));`
`       } else if (extra.indexOf('fflc') != -1) {`
`           info.push(this.makeInfoString('曾參與', pageLink[1], 'Wikipedia:特色列表评选/'`
`               + page, '特色列表评选', null));`
`       } else if (extra.indexOf('fgan') != -1) {`
`           info.push(this.makeInfoString('曾參與', pageLink[1], 'Wikipedia:優良條目候選',`
`               '優良條目候選', null));`
`       }`
`       return info;`
`   },`
`   /**`
`    * Get the correct link for Good Article reassessments. These things require an`
`    * additional AJAX request to determine whether it's a community or individual`
`    * reassessment. The trick is to assume it's a community reassessment, then`
`    * switch the link once the request returns if it's actually not.`
`    */`
`   getGARLink: function getGARLink (articleName, reviewNumber) {`
`       var communityTitle = 'Wikipedia:Good_article_reassessment\/' + articleName + '\/' + reviewNumber,`
`           individualTitle = 'Talk:' + articleName + '\/GA' + reviewNumber,`
`           url = mw.config.get('wgServer') + mw.config.get('wgScriptPath') + '\/api.php?action=query&titles='`
`               + communityTitle + '|' + individualTitle + '&prop=info&format=json';`
`       this.ajaxMain(url, this.getGARLinkCallback, [communityTitle, individualTitle]);`
`       return communityTitle;`
`   },`
`   /**`
`    * Now we have the information back from the API and need to figure out if the`
`    * link needs to be changed.`
`    */`
`   getGARLinkCallback: function getGARLinkCallback (request, altTitles) {`
`       if (request.readyState == 4 && request.status == 200) {`
`           var text = request.responseText;`
`           if (JSON && JSON.parse) {`
`               var query = JSON.parse(text)['query'];`
`           }`
`           else return;`
`           var communityTitleNorm, individualTitleNorm;`
`           if (query['normalized'] && query['normalized'].length == 2) {`
`               if (query['normalized'][0]['from'] == altTitles[0])`
`                   communityTitleNorm = query['normalized'][0]['to'];`
`               else if (query['normalized'][1]['from'] == altTitles[0])`
`                   communityTitleNorm = query['normalized'][1]['to'];`
`               if (query['normalized'][0]['from'] == altTitles[1])`
`                   individualTitleNorm = query['normalized'][0]['to'];`
`               else if (query['normalized'][1]['from'] == altTitles[1])`
`                   individualTitleNorm = query['normalized'][1]['to'];`
`           }`
`           else {`
`               communityTitleNorm = altTitles[0];`
`               individualTitleNorm = altTitles[1];`
`           }`
`           var noCommunityAssessment = false;`
`           for (var i = -1; i >= -2; i--) {`
`               if (query['pages'][i] && typeof query['pages'][i]['missing'] === 'string') {`
`                   if (query['pages'][i]['title'] == individualTitleNorm) {`
`                       // No individual assessment, no need to change anything.`
`                       return;`
`                   }`
`                   else if (query['pages'][i]['title'] == communityTitleNorm) {`
`                       // There's no community assessment, so flag it.`
`                       noCommunityAssessment = true;`
`                   }`
`               }`
`           }`
`           var garLink = document.getElementById('assess-gar-link').getElementsByTagName('a')[0];`
`           if (noCommunityAssessment && garLink) {`
`               // There's an individual assessment but no community assessment.`
`               // Switch the link.`
`               garLink.setAttribute('href', mw.config.get('wgArticlePath').replace('$1', '') + altTitles[1]);`
`           }`
`       }`
`   },`
`   /**`
`    * Creates the peer review text from an info string, if a peer review was detected earlier.`
`    */`
`   addPeerReview: function addPeerReview (peerReview, activeReview) {`
`       var reviewText = null, path = mw.config.get('wgArticlePath').replace('$1', '');`
`       if (peerReview) {`
`           reviewText = (activeReview`
`               ? '当前正在`<a href="' + path + peerReview + '">`同行评审`</a>`。'`
`               : '曾经过 `<a href="' + path + peerReview + '">`同行评审`</a>`。');`
`           reviewText = '`<span class="assess-info-review">`' + reviewText + '`</span>`';`
`       }`
`       return reviewText;`
`   },`
`   /**`
`    * Updates article header with new assessment information by giving it a new`
`    * class (for style information such as color) and altering the tagline below`
`    * it to state the assessment found.`
`    * @param {String} newClass - the CSS class name added to the article header`
`    * @param {String} slogan - italicized text prepended to the tagline, showing`
`    *        the article's main assessment`
`    * @param {String} info - additional assessment info appended to the tagline`
`    * @static`
`    */`
`   update: function update (newClass, slogan, info) {`
`       var firstHeading = document.getElementsByTagName('h1')[0];`
`       var siteSub = '`<span class="assess-article-rating">`' + slogan + '<\/span>';`
`       siteSub += '—维基百科，自由的百科全书';`
`       if (info && info.length > 0) {`
`           siteSub += '`<span class="assess-info-all">`. '`
`               + (typeof info.join === 'undefined'`
`                   ? info.toString()`
`                   : info.join(' ')`
`               ) + '<\/span>';`
`       }`
`       firstHeading.className += ' ' + (typeof newClass.join === 'undefined'`
`           ? newClass.toString()`
`           : newClass.join(' ')`
`       ); // add newClass as additional class(es)`
`       document.getElementById('siteSub').innerHTML = siteSub;`
`   },`
`   /**`
`    * Creates a string formatted for the 'info' parameter in the update method.`
`    * @param start - text at the beginning of the string, before the link`
`    * @param pageLink - a link to the target page`
`    * @param defLink - the backup page link if !pageLink`
`    * @param linkText - the text of the link`
`    * @param end - text after the link`
`    * @return {String} output - the info string`
`    * @static`
`    */`
`   makeInfoString: function makeInfoString (start, pageLink, defLink, linkText, end) {`
`       var output;`
`       var path = mw.config.get('wgArticlePath').replace('$1', '');`
`       var page = pageLink ? path + pageLink : (defLink ? path + defLink : null);`
`       start = start ? start.toString() + ' ' : '';`
`       linkText = linkText ? linkText.toString() : '';`
`       end = end ? ' ' + end.toString() + '.' : '.';`
`       output = start + (page ? '<a href="' + page + '"' + (linkText ? '>' : ' \/>') : '')`
`           + linkText + ((page && linkText) ? '<\/a>' : '') + end;`
`       return output;`
`   },`
`   /**`
`    * Encodes the URL of a Wikipedia page for use in the talkAssess method.`
`    * @param {String} inputText - the unencoded full page name`
`    * @return {String} outputText - the encoded page name`
`    * @static`
`    */`
`   encodePageName: function encodePageName (inputText) {`
`       if (!inputText) return null;`
`       var outputText = encodeURIComponent(inputText);`
`       while (outputText != null && outputText.match(/(\%20|\%2F)/i)) {`
`           outputText = outputText.replace(/\%20/i, '_'); // unescape spaces for readability`
`           outputText = outputText.replace(/\%2F/i, '\/'); // %2F must be unescaped`
`       }`
`       return outputText;`
`   },`
`   callHooks: function callHooks (hook) {`
`       for (funct in this[hook]) {`
`           this[hook][funct].call(this);`
`       }`
`   },`
`   addHook: function addHook (hook, funct) {`
`       if (typeof this[hook] === 'undefined')`
`           this[hook] = [];`
`       this[hook][this[hook].length] = funct;`
`       return this;`
`   },`
`   /**`
`    * Decodes all HTML entities in the string provided.`
`    */`
`   decodeEntities: function decodeEntities (str) {`
`       var t = document.createElement("textarea");`
`       t.innerHTML = str;`
`       return t.value;`
`   }`

};

// Implement Array.indexOf for older browsers that don't have it if (\!Array.prototype.indexOf) {

`   Array.prototype.indexOf = function indexOf (elt, from) {`
`       var len = this.length >>> 0;`
`       var from = Number(arguments[1]) || 0;`
`       from = (from < 0) ? Math.ceil(from) : Math.floor(from);`
`       if (from < 0)`
`           from += len;`
`       for (; from < len; from++) {`
`           if (from in this && this[from] === elt)`
`               return from;`
`       }`
`       return -1;`
`   };`

}

// Implement String.trim for browsers that don't have it if (\!String.prototype.trim) {

`   String.prototype.trim = function trim () {`
`       var str = this.replace(/^\s\s*/, ''),`
`           ws = /\s/,`
`           i = str.length;`
`       while (ws.test(str.charAt(--i)));`
`       return str.slice(0, i + 1);`
`   }`

}

// Backwards compatibility MetadataScript = MetadataObject = assessment

/\*\*

`* Initializes the script on page load`
`*/`

if (mw.config.get('wgNamespaceNumber') == 0 && (mw.config.get('wgAction') == 'view' || mw.config.get('wgAction') == 'purge')

`       && document.location.href.search(/\?(.+\&)?printable=[^&]/i) == -1`
`       && mw.config.get('wgPageName') != 'Main_Page') {`
`   $(function () {`
`       if (assessment.autorun)`
`           assessment.init();`
`   });`

}

importScript('User:Shizhao/projectbanners.js');