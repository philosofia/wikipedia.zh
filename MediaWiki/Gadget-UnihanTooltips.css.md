.unihantooltip {

`       position: absolute;`
`       list-style: none;`
`       list-style-image: none;`
`       opacity: 0;`
`       font-size: small;`
`       margin: 0;`
`       z-index: 5;`
`       padding: 0;`

} .unihantooltip li {

`       border: #a2a9b1 2px solid;`
`       max-width: 260px;`
`       padding: 10px 8px 13px 8px;`
`       margin: 0px;`
`       background-color: #F8F9FA;`
`       box-shadow: 2px 4px 2px rgba(0,0,0,0.3);`
`       -moz-box-shadow: 2px 4px 2px rgba(0,0,0,0.3);`
`       -webkit-box-shadow: 2px 4px 2px rgba(0,0,0,0.3);`

} .unihantooltip li+li {

`       margin-left: 7px;`
`       margin-top: -2px;`
`       border: 0;`
`       padding: 0;`
`       height: 3px;`
`       width: 0px;`
`       background-color: transparent;`
`       box-shadow: none;`
`       -moz-box-shadow: none;`
`       -webkit-box-shadow: none;`
`       border-top: 12px #a2a9b1 solid;`
`       border-right: 7px transparent solid;`
`       border-left: 7px transparent solid;`

} .unihantooltip\>li+li::after {

`       content: '';`
`       border-top: 8px #F7F7F7 solid;`
`       border-right: 5px transparent solid;`
`       border-left: 5px transparent solid;`
`       margin-top: -12px;`
`       margin-left: -5px;`
`       z-index: 1;`
`       height: 0px;`
`       width: 0px;`
`       display: block;`

} .client-js body .unihantooltip li li {

`       border: none;`
`       box-shadow: none;`
`       -moz-box-shadow: none;`
`       -webkit-box-shadow: none;`
`       height: auto;`
`       width: auto;`
`       margin: auto;`
`       padding: 0;`
`       position: static;`

} .UHflipped {

`       padding-top: 13px;`

} .unihantooltip.UHflipped li+li {

`       position: absolute;`
`       top: 2px;`
`       border-top: 0;`
`       border-bottom: 12px #a2a9b1 solid;`

} .unihantooltip.UHflipped li+li::after {

`       border-top: 0;`
`       border-bottom: 8px #F7F7F7 solid;`
`       position: absolute;`
`       margin-top: 7px;`

} .UHsettings{

`       float: right;`
`       height: 16px;`
`       width: 16px;`
`       cursor: pointer;`
`       background-image: url(//upload.wikimedia.org/wikipedia/commons/thumb/7/77/Gear_icon.svg/24px-Gear_icon.svg.png);`
`       background-image: linear-gradient(transparent, transparent), url(//upload.wikimedia.org/wikipedia/commons/7/77/Gear_icon.svg);`
`       margin-top: -9px;`
`       margin-right: -7px;`
`       -webkit-transition: opacity 0.15s;`
`       -moz-transition: opacity 0.15s;`
`       -o-transition: opacity 0.15s;`
`       -ms-transition: opacity 0.15s;`
`       transition: opacity 0.15s;`
`       opacity: 0.6;`
`       filter: alpha(opacity=60);`

} .UHsettings:hover{

`       opacity: 1;`
`       filter: alpha(opacity=100);`

} .UHTarget{

`       border: #a2a9b1 2px solid;`

}