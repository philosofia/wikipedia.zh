/\*

## 折叠效果

  - /

/\* Standard Navigationsleisten.\*/

div.Boxmerge, div.NavFrame {

`       margin: 0px;`
`       padding: 2px;`
`       border: 1px solid #aaaaaa;`
`       border-collapse: collapse;`
`       font-size: 95%;`

} div.Boxmerge div.NavFrame {

`       border-style: none;`
`       border-style: hidden;`

} div.NavFrame + div.NavFrame, div.NavFrame + table.collapsible,
table.collapsible + div.NavFrame, table.collapsible + table.collapsible
{

`       border-top-style: none;`
`       border-top-style: hidden;`

} div.NavPic {

`       background-color: #ffffff;`
`       margin: 0px;`
`       padding: 2px;`
`       float: left;`

} div.NavFrame div.NavHead {

`       min-height: 1.6em;`
`       font-weight: bold;`
`       font-size: 100%;`
`       text-align: center;`
`       background-color: #efefef;`
`       cursor:pointer;`

} div.NavFrame p {

`       font-size: 100%;`

} div.NavFrame div.NavContent {

`       font-size: 100%;`

} div.NavFrame div.NavContent p {

`       font-size: 100%;`

} div.NavEnd {

`       margin: 0px;`
`       padding: 0px;`
`       line-height: 1px;`
`       clear: both;`

} span.NavToggle {

`       float: right;`
`       /*保证在禁用JS状态下不显示提示，使用hidden以保证在navbox标题能占有宽度*/`
`       visibility: hidden;`
`       text-align: right;`
`       font-weight: normal;`
`       font-size: 80%;`

}