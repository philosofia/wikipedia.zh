if ( mw.config.get( 'wgNamespaceNumber' ) \!== 0 ) {

`   customizeToolbar( function() {`
`       this.wikiEditor('addToToolbar', {`
`           'sections': {`
`               'votes': {`
`                   'type': 'toolbar', // Can also be 'booklet'`
`                   'label': '投票讨论'`
`                   // or 'labelMsg': 'section-emoticons-label' for a localized label`
`               }`
`           }`
`       } );`

`       // To add a group to an existing toolbar section:`
`       this.wikiEditor('addToToolbar', {`
`           'section': 'votes',`
`           'groups': {`
`               'vote': {`
`               }`
`           }`
`       } );`
`       this.wikiEditor('addToToolbar', {`
`           'section': 'votes',`
`           'group': 'vote',`
`           'tools': {`
`               'support': {`
`                   label: '支持',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/9/94/Symbol_support_vote.svg/22px-Symbol_support_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'oppose': {`
`                   label: '反对',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/7/7f/Symbol_oppose_vote.svg/22px-Symbol_oppose_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'neutral': {`
`                   label: '中立',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/8/89/Symbol_neutral_vote.svg/22px-Symbol_neutral_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               }`
`           }`
`       } );`

`       this.wikiEditor('addToToolbar', {`
`           'section': 'votes',`
`           'groups': {`
`               'othervote': {`
`               }`
`           }`
`       } );`

`       this.wikiEditor('addToToolbar', {`
`           'section': 'votes',`
`           'group': 'othervote',`
`           'tools': {`
`               'comment': {`
`                   label: '意见',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Symbol_opinion_vote.svg/22px-Symbol_opinion_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'suggestion': {`
`                   label: '建议',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Symbol_suggestion_vote.svg/22px-Symbol_suggestion_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'reply': {`
`                   label: '回应',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/d/da/Symbol_reply_vote.svg/22px-Symbol_reply_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'remind': {`
`                   label: '提醒',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/8/89/Symbol_remind_vote.svg/22px-Symbol_remind_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'note': {`
`                   label: '注意',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/c/c1/Symbol_note_vote.svg/22px-Symbol_note_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'helpneeded': {`
`                   label: '求助',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/c/cc/Symbol_question_vote_3.svg/22px-Symbol_question_vote_3.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'question': {`
`                   label: '疑问/问题',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/1/11/Symbol_question_vote.svg/22px-Symbol_question_vote.svg.png',`
`                   action: {`
`                   type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               }`
`           }`
`       } );`

`       this.wikiEditor('addToToolbar', {`
`           'section': 'votes',`
`           'groups': {`
`               'vfd': {`
`                   'label': '存废讨论'`
`               }`
`           }`
`       } );`
`       this.wikiEditor('addToToolbar', {`
`           'section': 'votes',`
`           'group': 'vfd',`
`           'tools': {`
`               'vk': {`
`                   label: '保留',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Symbol_kept_vote.svg/22px-Symbol_kept_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'vsk': {`
`                   label: '快速保留',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Symbol_keep_vote.svg/22px-Symbol_keep_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'vtk': {`
`                   label: '暂时保留',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/6/6c/Time2wait.svg/22px-Time2wait.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'vd': {`
`                   label: '删除',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/8/89/Symbol_delete_vote.svg/22px-Symbol_delete_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'vsd': {`
`                   label: '快速删除',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Symbol_speedy_delete_vote.svg/22px-Symbol_speedy_delete_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'vm': {`
`                   label: '合并',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/b/b0/Symbol_merge_vote.svg/22px-Symbol_merge_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'vmp': {`
`                   label: '移动',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/5/50/Symbol_move_vote.svg/22px-Symbol_move_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'vmu': {`
`                   label: '移动到用户页',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/f/f4/Symbol_userfy_vote.svg/22px-Symbol_userfy_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`
`        `
`               'vr': {`
`                   label: '重定向',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/3/30/Symbol_deferred.svg/22px-Symbol_deferred.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'transwiki': {`
`                   label: '迁移到姊妹计划',`
`                   type: 'select',`
`                   list: {`
`                       'vmb' : {`
`                           label: '迁移到维基教科书',`
`                           action: {`
`                               type: 'encapsulate',`
`                               options: {`
`                                   pre: '``',`
`                                   periMsg: '填写理由', `
`                                   post: '--~~\~~'`
`                               }`
`                           }`
`                       }, `
`                       'vmd' : {`
`                           label: '迁移到维基词典',`
`                           action: {`
`                               type: 'encapsulate',`
`                               options: {`
`                                   'pre': '``',`
`                                   periMsg: '填写理由', `
`                                   post: '--~~\~~'`
`                               }`
`                           }`
`                       }, `
`                       'vms' : {`
`                           label: '迁移到维基文库',`
`                           action: {`
`                               type: 'encapsulate',`
`                               options: {`
`                                   pre: '``',`
`                                   periMsg: '填写理由', `
`                                   post: '--~~\~~'`
`                               }`
`                           }`
`                       }, `
`                       'vmq' : {`
`                           label: '迁移到维基语录',`
`                           action: {`
`                               type: 'encapsulate',`
`                               options: {`
`                                   pre: '``',`
`                                   periMsg: '填写理由', `
`                                   post: '--~~\~~'`
`                               }`
`                           }`
`                       }, `
`                       'vmc' : {`
`                           label: '迁移到維基共享資源',`
`                           action: {`
`                               type: 'encapsulate',`
`                               options: {`
`                                   pre: '``',`
`                                   periMsg: '填写理由', `
`                                   post: '--~~\~~'`
`                               }`
`                           }`
`                       }, `
`                       'vmvoy' : {`
`                           label: '迁移到維基导游',`
`                           action: {`
`                               type: 'encapsulate',`
`                               options: {`
`                                   pre: '``',`
`                                   periMsg: '填写理由', `
`                                   post: '--~~\~~'`
`                               }`
`                           }`
`                       }`
`                   }`
`               }`
`           }`
`       } );`

`       this.wikiEditor('addToToolbar', {`
`           'section': 'votes',`
`           'groups': {`
`               'other': {`
`                   'label': '其他'`
`               }`
`           }`
`       } );`
`       this.wikiEditor('addToToolbar', {`
`           'section': 'votes',`
`           'group': 'other',`
`           'tools': {`
`               'possible': {`
`                   label: '可能',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Symbol_possible_vote.svg/22px-Symbol_possible_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'buchong': {`
`                   label: '補充',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/3/30/Symbol_dot_dot_dot.svg/22px-Symbol_dot_dot_dot.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'notvote': {`
`                   label: '這不是投票',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/6/61/Symbol_abstain_vote.svg/22px-Symbol_abstain_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'thx': {`
`                   label: '谢谢你',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/7/72/Emoticon_smile.svg/22px-Emoticon_smile.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               },`

`               'orz': {`
`                   label: '囧',`
`                   type: 'button',`
`                   icon: '//upload.wikimedia.org/wikipedia/commons/thumb/e/e3/Symbol_%E5%9B%A7_vote.svg/22px-Symbol_%E5%9B%A7_vote.svg.png',`
`                   action: {`
`                       type: 'encapsulate',`
`                       options: {`
`                           pre: "``",`
`                           periMsg: '填写理由', `
`                           post: '--~~\~~'`
`                       }`
`                   }`
`               }`
`           }`
`       } );`
`   } );`

}