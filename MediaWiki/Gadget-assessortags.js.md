/\*

```
 *
 * from [[:en:User:Drilnoth/assessortags.js|:en:User:Drilnoth/assessortags.js]]
 */

importScript('User:Jimmy_xu_wrk/Friendly/morebits.js');

//See [[User:Drilnoth/assessortags.js/doc|User:Drilnoth/assessortags.js/doc]] for details.
//Greatly based off of [[User:Ioeth/friendlytag.js|User:Ioeth/friendlytag.js]].
// <nowiki>
// If assessortagsConfig aint exist.
if( typeof( assessortagsConfig ) == 'undefined' ) {
    assessortagsConfig = {};
}

/**
 assessortagsConfig.summaryAd ( string )
 If ad should be added or not to summary, default "，通過[[Wikipedia:維基百科工具/維基專題標記|維基專題標記]]"
 */
if( typeof( assessortagsConfig.summaryAd ) == 'undefined' ) {
    assessortagsConfig.summaryAd = "，通過[[Wikipedia:維基百科工具/維基專題標記|維基專題標記]]";
}

/**
 assessortagsConfig.groupByDefault ( boolean )
 */
if( typeof( assessortagsConfig.groupByDefault ) == 'undefined' ) {
    assessortagsConfig.groupByDefault = true;
}

/**
 assessortagsConfig.groupingBanner ( choice between WikiProjectBanners and WikiProjectBannerShell )
 */
if( typeof( assessortagsConfig.groupingBanner ) == 'undefined' ) {
    assessortagsConfig.groupingBanner = "WikiProjectBannerShell";
}

/**
 assessortagsConfig.markTaggedPagesAsMinor ( boolean )
 */
if( typeof( assessortagsConfig.markTaggedPagesAsMinor ) == 'undefined' ) {
    assessortagsConfig.markTaggedPagesAsMinor = true;
}

function assessortags() {
    if( mw.config.get('wgNamespaceNumber') == 1 || mw.config.get('wgNamespaceNumber') == 5 || mw.config.get('wgNamespaceNumber') == 7 || mw.config.get('wgNamespaceNumber') == 11 || mw.config.get('wgNamespaceNumber') == 13 ||mw.config.get('wgNamespaceNumber') == 15 || mw.config.get('wgNamespaceNumber') == 101 )
    mw.util.addPortletLink( 'p-cactions', "javascript:assessortags.callback()", "维基专题", "ca-wikiprojecttags", "增加维基专题横幅", "");
}

$.when($.ready,mw.loader.using('mediawiki.util')).then(assessortags);

assessortags.callback = function assessortagsCallback() {
    var Window = new SimpleWindow( 400, 500 );
    var form = new QuickForm( assessortags.callback.evaluate );

    {
        Window.setTitle( "添加维基专题标记" );

        form.append( {
                type: 'checkbox',
                list: [
                    {
                        label: '合并到{{' + assessortagsConfig.groupingBanner + '}}',
                        value: 'group',
                        name: 'group',
                        tooltip: '如果增加2个以上横幅并勾选本项，所有新添加的横幅都将合并到一个{{' + assessortagsConfig.groupingBanner + '}}模板，由於一個未知的Bug，請勿取消勾选本项。',
                        checked: assessortagsConfig.groupByDefault
                    }
                ]
            }
        );

        form.append( { type:'submit' } );

        if( typeof( assessortagsConfig.customBannerList ) == 'object' ) {
            form.append( { type:'header', label:'Custom' } );
            form.append( { type: 'checkbox', name: 'custom', list: assessortagsConfig.customBannerList } );
            form.append( { type:'submit' } );
        }

        form.append( { type:'header', label:'维基专题横幅 (按主题)' } );
        form.append( { type:'checkbox', name: 'main', list: assessortags.mainList } );

        form.append( { type:'header', label:'维基专题横幅 (其他)' } );
        form.append( { type:'checkbox', name: 'second', list: assessortags.secondList } );
    }

    form.append( { type:'submit' } );

    var result = form.render();
    Window.setContent( result );
    Window.display();
}

assessortags.mainList = [
    {
        label: 'LGBT',
        value: 'LGBTProject',
        subgroup: {
            name: 'lgbt',
            type: 'checkbox',
            list: [
                {
                    label: "正在请求同行评审",
                    value: "|peer-review=yes"
                },
                {
                    label: "完成同行评审",
                    value: "|old-peer-review=yes"
                }
            ]
        }
    },
    {
        label: '人物传记',
        value: 'WPBiography',
        subgroup: {
            name: 'biography',
            type: 'checkbox',
            list: [
                {
                    label: "科学家专题",
                    value: "|s&a-work-group=yes"
                },
                {
                    label: "在世人物",
                    value: "|living=yes",
                    tooltip: 'Check box if person is alive, otherwise check box below.'
                },
                {
                    label: "已经逝世",
                    value: "|living=no",
                    tooltip: 'Check box if person is no longer alive, otherwise check box above.'
                },
                {
                    label: "需要关注",
                    value: "|attention=yes"
                },
                {
                    label: "需要信息框",
                    value: "|needs-infobox=yes"
                },
                {
                    label: "需要图片",
                    value: "|needs-photo=yes"
                },
            ]
        }
    },
    {
        label: '北京',
        value: '北京专题',
        subgroup: {
            name: 'beijing',
            type: 'checkbox',
            list: [
                {
                    label: "需要立即受到关注",
                    value: "|attention =yes"
                },
                {
                    label: "需要加入信息框",
                    value: "|needs-infobox=yes"
                },
                {
                    label: "需要更多来源",
                    value: "|ref=yes"
                }
            ]
        }
    },
    {
        label: '年号',
        value: '年号专题',
        },
    {
        label: '欧洲历史',
        value: '欧洲历史专题',
        subgroup: {
            name: 'euro',
            type: 'checkbox',
            list: [
                {
                    label: "需要立即受到关注",
                    value: "|attention=yes"
                },
                {
                    label: "需要加入信息框",
                    value: "|needs-infobox=yes"
                },
                {
                    label: "需要更多来源",
                    value: "|ref=yes"
                }
            ]
        }
    },
    {
        label: '水浒传',
        value: '水浒传专题',
    },
    {
        label: '电子游戏',
        value: 'WikiProject Video games',
        subgroup: {
            name: 'videogames',
            type: 'checkbox',
            list: [
                {
                    label: "需要立即受到关注",
                    value: "|attention=yes"
                },
                {
                    label: "需要加入信息框",
                    value: "|needs-infobox=yes"
                },
                {
                    label: "需要封面或图标",
                    value: "|cover=yes"
                },
                {
                    label: "需要截图或图片",
                    value: "|screenshot=yes"
                },
                {
                    label: "正在接受同行评审",
                    value: "|peer=yes"
                },
                {
                    label: "已接受过同行评审",
                    value: "|old-peer=yes"
                }
            ]
        }
    },
    {
        label: '台灣',
        value: '台灣專題',
        subgroup: {
            name: 'taiwan',
            type: 'checkbox',
            list: [
                {
                    label: "需要立即受到關注",
                    value: "|attention=yes"
                },
                {
                    label: "需要加入信息框",
                    value: "|needs-infobox=yes"
                },
                {
                    label: "需要更多來源",
                    value: "|ref=yes"
                }
            ]
        }
    },
    {
        label: '英格兰',
        value: 'WikiProject England',
    },
    {
        label: '太平洋颱風季',
        value: 'WikiProject PTS',
    },
    {
        label: '足球',
        value: '足球專題',
        subgroup: {
            name: 'football',
            type: 'checkbox',
            list: [
                {
                    label: "正在請求同行評審",
                    value: "|Peer-review=yes"
                },
                {
                    label: "已完成同行評審",
                    value: "|Old peer-review=yes"
                }
            ]
        }
    },
    {
        label: '電影',
        value: 'WPFilm',
    },
    {
        label: 'ACG',
        value: 'WikiProject ACG',
    },
    {
        label: '漢字文化圈',
        value: 'WikiProject Sinosphere',
    },
    {
        label: '日本',
        value: 'WikiProject Japan',
    },
    {
        label: '基礎條目',
        value: 'Vital',
    },
    {
        label: '中文領域基礎條目',
        value: 'Cba/level',
    },
    {
        label: '模仿 (提交後請編輯條目以修正參數)',
        value: 'FAOL',
    },
    {
                label: '第九次動員令作品',
                value: 'DC9/talk',
                tooltip: '請點選此選項以標記第九次動員令作品，同時請點選下面屬於本條目的兩個選項',
                subgroup: {
                        name: 'DC9',
                        type: 'checkbox',
                        list: [
                                {
                                        label: "達標條目",
                                        value: "|type=達",
                                        tooltip: '達標條目'
                                },
                                {
                                        label: "新條目推薦",
                                        value: "|type=新",
                                        tooltip: '新條目推薦'
                                },
                                {
                                        label: "優良條目",
                                        value: "|type=GA",
                                        tooltip: '優良條目作品'
                                },
                                {
                                        label: "特色條目",
                                        value: "|type=FA",
                                        tooltip: '特色條目作品'
                                },
                                {
                                        label: "特色列表",
                                        value: "|type=FL",
                                        tooltip: '特色列表作品'
                                },
                                {
                                        label: "大動員令",
                                        value: "|topic=大",
                                        tooltip: '第九次動員令 > 大動員令'
                                },
                                {
                                        label: "人文與社會科學",
                                        value: "|topic=人",
                                        tooltip: '第九次動員令 > 中動員令 > 人文與社會科學'
                                },
                                {
                                        label: "世界各地",
                                        value: "|topic=世",
                                        tooltip: '第九次動員令 > 中動員令 > 世界各地'
                                },
                                {
                                        label: "最多語言待撰條目",
                                        value: "|topic=最",
                                        tooltip: '第九次動員令 > 小動員令 > 最多語言待撰條目'
                                },
                                {
                                        label: "自然與自然科學",
                                        value: "|topic=自",
                                        tooltip: '第九次動員令 > 小動員令 > 自然與自然科學'
                                },
                                {
                                        label: "工程、技術與應用科學",
                                        value: "|topic=工",
                                        tooltip: '第九次動員令 > 小動員令 > 工程、技術與應用科學'
                                },
                                {
                                        label: "外交",
                                        value: "|topic=外",
                                        tooltip: '第九次動員令 > 小動員令 > 外交'
                                },
                        ]
                }
        },
];

assessortags.secondList = [
];

assessortags.callbacks = {
    main: function( self ) {
        var form = self.responseXML.getElementById( 'editform' );
        var tagRe, text = '', summaryText = ''; //Is the summaryText still needed?
        var tags = new Array(), groupableTags = new Array(); //Is the groupableTags really still needed? Removing it fowls stuff up, but it seems like it should be removable

        // Check for preexisting tags
        Status.info( '信息', '檢查已有模板' );
        for( var i = 0; i < self.params.tags.length; i++ ) {
            tagRe = new RegExp( '(\\{\\{' + self.params.tags[i] + '(\\||\\}\\}))', 'im' );
            if( !tagRe.exec( form.wpTextbox1.value ) ) {
                tags = tags.concat( self.params.tags[i] );
            } else {
                Status.info( 'Info', 'Found \{\{' + self.params.tags[i]
                    + '\}\} on the article already...excluding' );
            }
        }

        if( self.params.group && tags.length >= 2 ) {
            Status.info( '信息', '添加横幅到页面顶部' );
            Status.info( '信息', '正在將模板合併至 \{\{' + assessortagsConfig.groupingBanner + '\}\}' );

            groupableTags.sort();
            text += '\{\{' + assessortagsConfig.groupingBanner + '|1=' + '\n';
            for( var i = 0; i < tags.length; i++ ) {
                text += '\{\{' + tags[i];

                if( tags[i] == 'LGBTProject' ) {
                    text += self.params.lgbtSubcategory.join("");
                } else if( tags[i] == '北京专题' ) {
                    text += self.params.beijingSubcategory.join("");
                } else if( tags[i] == '欧洲历史专题' ) {
                    text += self.params.euroSubcategory.join("");
                } else if( tags[i] == 'WikiProject Video games' ) {
                    text += self.params.videogamesSubcategory.join("");
                } else if( tags[i] == '台灣專題' ) {
                    text += self.params.taiwanSubcategory.join("");
                } else if( tags[i] == '足球專題' ) {
                    text += self.params.footballSubcategory.join("");
                }
                text += '\}\}\n';
            }
            text += '\}\}\n';
        } else {
            tags = tags.concat( groupableTags );
        }

        if( self.params.group && tags.length < 2 ) {
            Status.info( '信息', '正在新增模板到本頁頂' );

            tags.sort();
            for( var i = 0; i < tags.length; i++ ) {
                text += '\{\{' + tags[i];
                if( tags[i] == 'LGBTProject' ) {
                    text += self.params.lgbtSubcategory.join("");
                } else if( tags[i] == '北京专题' ) {
                    text += self.params.beijingSubcategory.join("");
                } else if( tags[i] == '欧洲历史专题' ) {
                    text += self.params.euroSubcategory.join("");
                } else if( tags[i] == 'WikiProject Video games' ) {
                    text += self.params.videogamesSubcategory.join("");
                } else if( tags[i] == '台灣專題' ) {
                    text += self.params.taiwanSubcategory.join("");
                } else if( tags[i] == '足球專題' ) {
                    text += self.params.footballSubcategory.join("");
                }
                text += '\}\}\n';
            }
        }

        text += form.wpTextbox1.value;
        summaryText += '添加维基专题横幅到页面' + assessortagsConfig.summaryAd;

        var postData = {
            'wpMinoredit': assessortagsConfig.markTaggedPagesAsMinor ? 1 : undefined,
            'wpStarttime': form.wpStarttime.value,
            'wpEdittime': form.wpEdittime.value,
            'wpAutoSummary': form.wpAutoSummary.value,
            'wpEditToken': form.wpEditToken.value,
            'wpSummary': summaryText,
            'wpTextbox1': text
        };

        self.post( postData );
    }
}

assessortags.callback.evaluate = function assessortagsCallbackEvaluate(e) {
    var form = e.target;
    {if( typeof( assessortagsConfig.customBannerList ) == 'object' ) {
            var tags = form.getChecked( 'main' ).concat( form.getChecked( 'second' ) ).concat( form.getChecked( 'custom' ) );
        } else {
            var tags = form.getChecked( 'main' ).concat( form.getChecked( 'second' ) );
        }
        var lgbtSubcategory = form.getChecked( 'main.lgbt' );
        var beijingSubcategory = form.getChecked( 'main.beijing' );
        var euroSubcategory = form.getChecked( 'main.euro' );
        var videogamesSubcategory = form.getChecked( 'main.videogames' );
        var taiwanSubcategory = form.getChecked( 'main.taiwan' );
        var footballSubcategory = form.getChecked( 'main.football' );
    }
    var params;

    if( tags.length == 0 ) {
        alert( '請選擇最少一個模板。' );
        return;
    }
    params = {
        tags: tags,
        group: form.group.checked,
        lgbtSubcategory: lgbtSubcategory ? lgbtSubcategory : null,
        beijingSubcategory: beijingSubcategory ? beijingSubcategory : null,
        euroSubcategory: euroSubcategory ? euroSubcategory : null,
        videogamesSubcategory: videogamesSubcategory ? videogamesSubcategory : null,
        taiwanSubcategory: taiwanSubcategory ? taiwanSubcategory : null,
        footballSubcategory: footballSubcategory ? footballSubcategory : null,
        rcid: QueryString.exists( 'rcid' ) ? QueryString.get( 'rcid' ) : ''
        }

    Status.init( form );

    var query = {
        'title': mw.config.get('wgPageName'),
        'action': 'submit'
    };
    Wikipedia.actionCompleted.redirect = mw.config.get('wgPageName');
    Wikipedia.actionCompleted.notice = "标记完成，重新载入页面";
    var wikipedia_wiki = new Wikipedia.wiki( '條目修改', query, assessortags.callbacks.main );
    wikipedia_wiki.params = params;
    wikipedia_wiki.get();
}
// </nowiki>
//
```

[Category:维基脚本](https://zh.wikipedia.org/wiki/Category:维基脚本 "wikilink")