# **目次**

- [<ins>共用</ins>](#ins%E5%85%B1%E7%94%A8ins)
  - [<ins>共用組件</ins>](#ins%E5%85%B1%E7%94%A8%E7%B5%84%E4%BB%B6ins)
    - [<ins>錯誤訊息(ErrorMsg)</ins>](#ins%E9%8C%AF%E8%AA%A4%E8%A8%8A%E6%81%AFerrormsgins)
      - [屬性（Props）](#%E5%B1%AC%E6%80%A7props)
      - [範例](#%E7%AF%84%E4%BE%8B)
    - [<ins>標籤(Label)</ins>](#ins%E6%A8%99%E7%B1%A4labelins)
      - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props)
      - [預設屬性 (Default Props)](#%E9%A0%90%E8%A8%AD%E5%B1%AC%E6%80%A7-default-props)
      - [範例](#%E7%AF%84%E4%BE%8B-1)
    - [<ins>表單(Form)</ins>](#ins%E8%A1%A8%E5%96%AEformins)
      - [屬性（Props）](#%E5%B1%AC%E6%80%A7props-1)
      - [功能](#%E5%8A%9F%E8%83%BD)
      - [範例](#%E7%AF%84%E4%BE%8B-2)
    - [<ins>輸入框(inputs)</ins>](#ins%E8%BC%B8%E5%85%A5%E6%A1%86inputsins)
      - [Input 元件](#input-%E5%85%83%E4%BB%B6)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-1)
        - [預設屬性 (Default Props)](#%E9%A0%90%E8%A8%AD%E5%B1%AC%E6%80%A7-default-props-1)
        - [範例](#%E7%AF%84%E4%BE%8B-3)
      - [PwdInput 元件](#pwdinput-%E5%85%83%E4%BB%B6)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-4)
        - [範例](#%E7%AF%84%E4%BE%8B-6)
          - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-2)
          - [檢核訊息提示 (自身)](#%E6%AA%A2%E6%A0%B8%E8%A8%8A%E6%81%AF%E6%8F%90%E7%A4%BA-%E8%87%AA%E8%BA%AB)
          - [檢核訊息提示 (外部組件)](#%E6%AA%A2%E6%A0%B8%E8%A8%8A%E6%81%AF%E6%8F%90%E7%A4%BA-%E5%A4%96%E9%83%A8%E7%B5%84%E4%BB%B6)
      - [TextInput 元件](#textinput-%E5%85%83%E4%BB%B6)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-5)
        - [範例](#%E7%AF%84%E4%BE%8B-7)
          - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-3)
          - [檢核訊息提示 (自身)](#%E6%AA%A2%E6%A0%B8%E8%A8%8A%E6%81%AF%E6%8F%90%E7%A4%BA-%E8%87%AA%E8%BA%AB-1)
          - [檢核訊息提示 (外部組件)](#%E6%AA%A2%E6%A0%B8%E8%A8%8A%E6%81%AF%E6%8F%90%E7%A4%BA-%E5%A4%96%E9%83%A8%E7%B5%84%E4%BB%B6-1)
    - [<ins>單選框(Radio)</ins>](#ins%E5%96%AE%E9%81%B8%E6%A1%86radioins)
      - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-6)
        - [單選框 (Radio)](#%E5%96%AE%E9%81%B8%E6%A1%86-radio)
        - [單選框群組 (Radio.Group)](#%E5%96%AE%E9%81%B8%E6%A1%86%E7%BE%A4%E7%B5%84-radiogroup)
        - [單選框特殊樣式群組 (Radio.BtnGroup)](#%E5%96%AE%E9%81%B8%E6%A1%86%E7%89%B9%E6%AE%8A%E6%A8%A3%E5%BC%8F%E7%BE%A4%E7%B5%84-radiobtngroup)
      - [範例](#%E7%AF%84%E4%BE%8B-8)
        - [單獨使用單選框](#%E5%96%AE%E7%8D%A8%E4%BD%BF%E7%94%A8%E5%96%AE%E9%81%B8%E6%A1%86)
        - [單選框群組](#%E5%96%AE%E9%81%B8%E6%A1%86%E7%BE%A4%E7%B5%84)
        - [特別樣式的單選框群組](#%E7%89%B9%E5%88%A5%E6%A8%A3%E5%BC%8F%E7%9A%84%E5%96%AE%E9%81%B8%E6%A1%86%E7%BE%A4%E7%B5%84)
    - [<ins>下拉選單(Dropdown)</ins>](#ins%E4%B8%8B%E6%8B%89%E9%81%B8%E5%96%AEdropdownins)
      - [Dropdown 元件](#dropdown-%E5%85%83%E4%BB%B6)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-7)
        - [範例](#%E7%AF%84%E4%BE%8B-9)
          - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-4)
          - [自訂預設選項文字](#%E8%87%AA%E8%A8%82%E9%A0%90%E8%A8%AD%E9%81%B8%E9%A0%85%E6%96%87%E5%AD%97)
      - [DropdownCustom(Dropdown.Custom) 元件](#dropdowncustomdropdowncustom-%E5%85%83%E4%BB%B6)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-8)
        - [範例](#%E7%AF%84%E4%BE%8B-10)
          - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-5)
          - [自訂預設文字](#%E8%87%AA%E8%A8%82%E9%A0%90%E8%A8%AD%E6%96%87%E5%AD%97)
      - [DropDownCustomMenu(Dropdown.CustomMenu) 元件](#dropdowncustommenudropdowncustommenu-%E5%85%83%E4%BB%B6)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-9)
        - [範例](#%E7%AF%84%E4%BE%8B-11)
          - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-6)
          - [自訂預設文字和搜尋文字](#%E8%87%AA%E8%A8%82%E9%A0%90%E8%A8%AD%E6%96%87%E5%AD%97%E5%92%8C%E6%90%9C%E5%B0%8B%E6%96%87%E5%AD%97)
      - [DropDownCustomSearch(Dropdown.CustomSearch) 元件](#dropdowncustomsearchdropdowncustomsearch-%E5%85%83%E4%BB%B6)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-10)
        - [自定義選項物件 (options)](#%E8%87%AA%E5%AE%9A%E7%BE%A9%E9%81%B8%E9%A0%85%E7%89%A9%E4%BB%B6-options)
        - [範例](#%E7%AF%84%E4%BE%8B-12)
          - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-7)
          - [使用自定義選項結構](#%E4%BD%BF%E7%94%A8%E8%87%AA%E5%AE%9A%E7%BE%A9%E9%81%B8%E9%A0%85%E7%B5%90%E6%A7%8B)
      - [DropdownCurrency(Dropdown.Currency) 元件](#dropdowncurrencydropdowncurrency-%E5%85%83%E4%BB%B6)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-11)
        - [貨幣選項 (currencies)](#%E8%B2%A8%E5%B9%A3%E9%81%B8%E9%A0%85-currencies)
        - [onChange 回調函數 (onChange)](#onchange-%E5%9B%9E%E8%AA%BF%E5%87%BD%E6%95%B8-onchange)
        - [value 屬性](#value-%E5%B1%AC%E6%80%A7)
        - [範例](#%E7%AF%84%E4%BE%8B-13)
          - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-8)
          - [使用全部貨幣選項](#%E4%BD%BF%E7%94%A8%E5%85%A8%E9%83%A8%E8%B2%A8%E5%B9%A3%E9%81%B8%E9%A0%85)
          - [指定初始選擇的貨幣](#%E6%8C%87%E5%AE%9A%E5%88%9D%E5%A7%8B%E9%81%B8%E6%93%87%E7%9A%84%E8%B2%A8%E5%B9%A3)
    - [<ins>日期元件(DatePicker)</ins>](#ins%E6%97%A5%E6%9C%9F%E5%85%83%E4%BB%B6datepickerins)
      - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-12)
      - [範例](#%E7%AF%84%E4%BE%8B-14)
        - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-9)
        - [使用 prop 設定](#%E4%BD%BF%E7%94%A8-prop-%E8%A8%AD%E5%AE%9A)
      - [自定義日期格式 (`dateFormat`)](#%E8%87%AA%E5%AE%9A%E7%BE%A9%E6%97%A5%E6%9C%9F%E6%A0%BC%E5%BC%8F-dateformat)
      - [預設值 (`initValue`)](#%E9%A0%90%E8%A8%AD%E5%80%BC-initvalue)
      - [最小日期和最大日期 (`minDate` 和 `maxDate`)](#%E6%9C%80%E5%B0%8F%E6%97%A5%E6%9C%9F%E5%92%8C%E6%9C%80%E5%A4%A7%E6%97%A5%E6%9C%9F-mindate-%E5%92%8C-maxdate)
      - [自定義 CSS 類名 (`className`)](#%E8%87%AA%E5%AE%9A%E7%BE%A9-css-%E9%A1%9E%E5%90%8D-classname)
      - [自定義提示文字 (`spantext`)](#%E8%87%AA%E5%AE%9A%E7%BE%A9%E6%8F%90%E7%A4%BA%E6%96%87%E5%AD%97-spantext)
      - [禁用日期選擇元件 (`disabled` 和 `keydisabled`)](#%E7%A6%81%E7%94%A8%E6%97%A5%E6%9C%9F%E9%81%B8%E6%93%87%E5%85%83%E4%BB%B6-disabled-%E5%92%8C-keydisabled)
      - [取得選擇的日期 (`getValue`)](#%E5%8F%96%E5%BE%97%E9%81%B8%E6%93%87%E7%9A%84%E6%97%A5%E6%9C%9F-getvalue)
      - [自定義日期選擇的過濾函數 (`filterDate`)](#%E8%87%AA%E5%AE%9A%E7%BE%A9%E6%97%A5%E6%9C%9F%E9%81%B8%E6%93%87%E7%9A%84%E9%81%8E%E6%BF%BE%E5%87%BD%E6%95%B8-filterdate)
    - [<ins>多選日期天數元件(DayPicker)</ins>](#ins%E5%A4%9A%E9%81%B8%E6%97%A5%E6%9C%9F%E5%A4%A9%E6%95%B8%E5%85%83%E4%BB%B6daypickerins)
      - [屬性（Props）](#%E5%B1%AC%E6%80%A7props-2)
      - [功能](#%E5%8A%9F%E8%83%BD-1)
      - [範例](#%E7%AF%84%E4%BE%8B-15)
    - [<ins>彈跳視窗元件(Modal)</ins>](#ins%E5%BD%88%E8%B7%B3%E8%A6%96%E7%AA%97%E5%85%83%E4%BB%B6modalins)
      - [屬性（Props）](#%E5%B1%AC%E6%80%A7props-3)
      - [範例](#%E7%AF%84%E4%BE%8B-16)
    - [<ins>虛擬鍵盤(KeyBoard)</ins>](#ins%E8%99%9B%E6%93%AC%E9%8D%B5%E7%9B%A4keyboardins)
      - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-13)
      - [全功能小鍵盤 (Full Keyboard)](#%E5%85%A8%E5%8A%9F%E8%83%BD%E5%B0%8F%E9%8D%B5%E7%9B%A4-full-keyboard)
      - [數字小鍵盤 (Numeric Keyboard)](#%E6%95%B8%E5%AD%97%E5%B0%8F%E9%8D%B5%E7%9B%A4-numeric-keyboard)
      - [使用 `withKeyboard` 高階組件 (HOC)](#%E4%BD%BF%E7%94%A8-withkeyboard-%E9%AB%98%E9%9A%8E%E7%B5%84%E4%BB%B6-hoc)
    - [<ins>泡泡框提示文字(tooltips)</ins>](#ins%E6%B3%A1%E6%B3%A1%E6%A1%86%E6%8F%90%E7%A4%BA%E6%96%87%E5%AD%97tooltipsins)
      - [Tooltip 泡泡提示框](#tooltip-%E6%B3%A1%E6%B3%A1%E6%8F%90%E7%A4%BA%E6%A1%86)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-14)
        - [使用示例](#%E4%BD%BF%E7%94%A8%E7%A4%BA%E4%BE%8B)
      - [衍生組件](#%E8%A1%8D%E7%94%9F%E7%B5%84%E4%BB%B6)
        - [BottomTooltip](#bottomtooltip)
        - [LeftTooltip](#lefttooltip)
        - [RightTooltip](#righttooltip)
        - [TopTooltip](#toptooltip)
    - [<ins>連結(Link)</ins>](#ins%E9%80%A3%E7%B5%90linkins)
      - [ICON_TYPE 常數](#icon_type-%E5%B8%B8%E6%95%B8)
      - [PhoneLink](#phonelink)
        - [屬性（Props）](#%E5%B1%AC%E6%80%A7props-4)
      - [HyperLink](#hyperlink)
        - [屬性（Props）](#%E5%B1%AC%E6%80%A7props-5)
      - [ImgLink](#imglink)
        - [屬性（Props）](#%E5%B1%AC%E6%80%A7props-6)
      - [IconLink](#iconlink)
        - [屬性（Props）](#%E5%B1%AC%E6%80%A7props-7)
    - [<ins>表格元件(Table)</ins>](#ins%E8%A1%A8%E6%A0%BC%E5%85%83%E4%BB%B6tableins)
      - [普通表格 (Table.Normal)](#%E6%99%AE%E9%80%9A%E8%A1%A8%E6%A0%BC-tablenormal)
        - [Table.Normal.A](#tablenormala)
          - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-15)
          - [範例](#%E7%AF%84%E4%BE%8B-17)
        - [Table.Normal.B](#tablenormalb)
          - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-16)
          - [範例](#%E7%AF%84%E4%BE%8B-18)
        - [Table.Normal.C](#tablenormalc)
          - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-17)
          - [範例](#%E7%AF%84%E4%BE%8B-19)
        - [Table.Normal.D](#tablenormald)
          - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-18)
          - [範例](#%E7%AF%84%E4%BE%8B-20)
      - [響應式表格 (Table.Responsive)](#%E9%9F%BF%E6%87%89%E5%BC%8F%E8%A1%A8%E6%A0%BC-tableresponsive)
        - [Table.Responsive.Card.A](#tableresponsivecarda)
          - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-19)
          - [範例](#%E7%AF%84%E4%BE%8B-21)
        - [Table.Responsive.Card.B](#tableresponsivecardb)
          - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-20)
          - [範例](#%E7%AF%84%E4%BE%8B-22)
      - [Table.Responsive.Card.C](#tableresponsivecardc)
        - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-21)
        - [範例](#%E7%AF%84%E4%BE%8B-23)
        - [Table.Responsive.Sticky.A](#tableresponsivestickya)
          - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-22)
          - [範例](#%E7%AF%84%E4%BE%8B-24)
    - [<ins>PDF元件(PdfGenerator)</ins>](#inspdf%E5%85%83%E4%BB%B6pdfgeneratorins)
      - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-23)
      - [範例](#%E7%AF%84%E4%BE%8B-25)
        - [使用 `downloadPdf` 方法：](#%E4%BD%BF%E7%94%A8-downloadpdf-%E6%96%B9%E6%B3%95)
        - [使用 `generatePdfByApi` 方法：](#%E4%BD%BF%E7%94%A8-generatepdfbyapi-%E6%96%B9%E6%B3%95)
        - [使用 `generatePdfByRef` 方法：](#%E4%BD%BF%E7%94%A8-generatepdfbyref-%E6%96%B9%E6%B3%95)
        - [使用 `generatePdfByElement` 方法：](#%E4%BD%BF%E7%94%A8-generatepdfbyelement-%E6%96%B9%E6%B3%95)
        - [使用 `generatePdfByFunction` 方法：](#%E4%BD%BF%E7%94%A8-generatepdfbyfunction-%E6%96%B9%E6%B3%95)
      - [Modal 屬性](#modal-%E5%B1%AC%E6%80%A7)
    - [<ins>分頁(Pagination)</ins>](#ins%E5%88%86%E9%A0%81paginationins)
      - [屬性 (Props)](#%E5%B1%AC%E6%80%A7-props-24)
      - [範例](#%E7%AF%84%E4%BE%8B-26)
    - [<ins>入口(Portal)</ins>](#ins%E5%85%A5%E5%8F%A3portalins)
      - [如何使用](#%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8)
      - [範例](#%E7%AF%84%E4%BE%8B-27)
      - [工作原理](#%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86)
    - [<ins>畫面遮罩(Loading)</ins>](#ins%E7%95%AB%E9%9D%A2%E9%81%AE%E7%BD%A9loadingins)
      - [使用方式](#%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F)
      - [屬性](#%E5%B1%AC%E6%80%A7)
      - [載入指示符和畫面遮罩](#%E8%BC%89%E5%85%A5%E6%8C%87%E7%A4%BA%E7%AC%A6%E5%92%8C%E7%95%AB%E9%9D%A2%E9%81%AE%E7%BD%A9)
      - [示例](#%E7%A4%BA%E4%BE%8B)
    - [<ins>列表(ListItem)</ins>](#ins%E5%88%97%E8%A1%A8listitemins)
      - [列表組件常數](#%E5%88%97%E8%A1%A8%E7%B5%84%E4%BB%B6%E5%B8%B8%E6%95%B8)
      - [列表組件的通用 propType](#%E5%88%97%E8%A1%A8%E7%B5%84%E4%BB%B6%E7%9A%84%E9%80%9A%E7%94%A8-proptype)
      - [列表組件的類型](#%E5%88%97%E8%A1%A8%E7%B5%84%E4%BB%B6%E7%9A%84%E9%A1%9E%E5%9E%8B)
  - [<ins>共用工具</ins>](#ins%E5%85%B1%E7%94%A8%E5%B7%A5%E5%85%B7ins)
    - [<ins>arithmeticHelper</ins>](#insarithmetichelperins)
      - [`getRandomNumber(min, max)`](#getrandomnumbermin-max)
      - [`generateArithmeticQuestion(operator)`](#generatearithmeticquestionoperator)
    - [<ins>blobHelpers</ins>](#insblobhelpersins)
      - [`downloadBlob(blob, filename = '')`](#downloadblobblob-filename--)
    - [<ins>browserHelpers</ins>](#insbrowserhelpersins)
      - [`getOperatingSystem()`](#getoperatingsystem)
      - [`getScreenResolution()`](#getscreenresolution)
      - [`getBrowserVersion()`](#getbrowserversion)
      - [`getJavaScriptVersion()`](#getjavascriptversion)
      - [`isBrowser64Bit()`](#isbrowser64bit)
      - [`getContextPath()`](#getcontextpath)
      - [`getTxnUrl(systemCode, categoryCode, functionCode, route = '/01')`](#gettxnurlsystemcode-categorycode-functioncode-route--01)
      - [`getStaticUrl(path)`](#getstaticurlpath)
    - [<ins>chipCardHelper</ins>](#inschipcardhelperins)
      - [`getChipCardErrorKeyByCode(code)`](#getchipcarderrorkeybycodecode)
    - [<ins>formatArray</ins>](#insformatarrayins)
      - [`fStrsToOneObj(arr, val)`](#fstrstooneobjarr-val)
    - [<ins>formatCheck</ins>](#insformatcheckins)
      - [字符串格式驗證函數](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%A0%BC%E5%BC%8F%E9%A9%97%E8%AD%89%E5%87%BD%E6%95%B8)
      - [資料類型檢查函數](#%E8%B3%87%E6%96%99%E9%A1%9E%E5%9E%8B%E6%AA%A2%E6%9F%A5%E5%87%BD%E6%95%B8)
      - [瀏覽器功能支持檢查函數](#%E7%80%8F%E8%A6%BD%E5%99%A8%E5%8A%9F%E8%83%BD%E6%94%AF%E6%8C%81%E6%AA%A2%E6%9F%A5%E5%87%BD%E6%95%B8)
      - [瀏覽器功能支持檢查函數](#%E7%80%8F%E8%A6%BD%E5%99%A8%E5%8A%9F%E8%83%BD%E6%94%AF%E6%8C%81%E6%AA%A2%E6%9F%A5%E5%87%BD%E6%95%B8-1)
    - [<ins>formatDate</ins>](#insformatdateins)
      - [`toIntOrStr(str)`](#tointorstrstr)
      - [`getTwLocaleString(time)`](#gettwlocalestringtime)
      - [`getYMDHMS(time, symbol = '/')`](#getymdhmstime-symbol--)
      - [`getYMD(time, symbol = '/')`](#getymdtime-symbol--)
      - [`getTwYMD(time, symbol = '')`](#gettwymdtime-symbol--)
    - [<ins>formatNumber</ins>](#insformatnumberins)
      - [`addThousandSeparator(str, separator = ',')`](#addthousandseparatorstr-separator--)
      - [`removeSymbol(str)`](#removesymbolstr)
    - [<ins>getApiResponse</ins>](#insgetapiresponseins)
      - [`getApiResponse(response)`](#getapiresponseresponse)
    - [<ins>getComponentDisplayName</ins>](#insgetcomponentdisplaynameins)
      - [`getComponentDisplayName(WrappedComponent)`](#getcomponentdisplaynamewrappedcomponent)
    - [<ins>type</ins>](#instypeins)
  - [<ins>自定義 Hooks 介紹</ins>](#ins%E8%87%AA%E5%AE%9A%E7%BE%A9-hooks-%E4%BB%8B%E7%B4%B9ins)
    - [<ins>useBreadcrumbs</ins>](#insusebreadcrumbsins)
      - [用法](#%E7%94%A8%E6%B3%95)
      - [功能](#%E5%8A%9F%E8%83%BD-2)
    - [<ins>useCountdown</ins>](#insusecountdownins)
      - [用法](#%E7%94%A8%E6%B3%95-1)
      - [功能](#%E5%8A%9F%E8%83%BD-3)
    - [<ins>useDebounce</ins>](#insusedebounceins)
      - [用法](#%E7%94%A8%E6%B3%95-2)
      - [功能](#%E5%8A%9F%E8%83%BD-4)
    - [<ins>useE2EE</ins>](#insusee2eeins)
      - [用法](#%E7%94%A8%E6%B3%95-3)
      - [功能](#%E5%8A%9F%E8%83%BD-5)
    - [<ins>useForm</ins>](#insuseformins)
      - [用法](#%E7%94%A8%E6%B3%95-4)
      - [功能](#%E5%8A%9F%E8%83%BD-6)
    - [<ins>useMenuDuplicateTxnRender</ins>](#insusemenuduplicatetxnrenderins)
      - [用法](#%E7%94%A8%E6%B3%95-5)
      - [功能](#%E5%8A%9F%E8%83%BD-7)
    - [<ins>useFrameResources</ins>](#insuseframeresourcesins)
      - [用法](#%E7%94%A8%E6%B3%95-6)
      - [功能](#%E5%8A%9F%E8%83%BD-8)
    - [<ins>useFrameDisableContextMenu</ins>](#insuseframedisablecontextmenuins)
      - [用法](#%E7%94%A8%E6%B3%95-7)
      - [功能](#%E5%8A%9F%E8%83%BD-9)
    - [<ins>useLoadTime</ins>](#insuseloadtimeins)
      - [用法](#%E7%94%A8%E6%B3%95-8)
      - [功能](#%E5%8A%9F%E8%83%BD-10)
    - [<ins>useLocalStorage</ins>](#insuselocalstorageins)
      - [用法](#%E7%94%A8%E6%B3%95-9)
      - [功能](#%E5%8A%9F%E8%83%BD-11)
      - [鍵的命名規定](#%E9%8D%B5%E7%9A%84%E5%91%BD%E5%90%8D%E8%A6%8F%E5%AE%9A)
      - [注意事項](#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85)
    - [<ins>usePageLoading</ins>](#insusepageloadingins)
      - [用法](#%E7%94%A8%E6%B3%95-10)
      - [功能](#%E5%8A%9F%E8%83%BD-12)
      - [注意事項](#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85-1)
    - [<ins>usePagination</ins>](#insusepaginationins)
      - [用法](#%E7%94%A8%E6%B3%95-11)
      - [功能](#%E5%8A%9F%E8%83%BD-13)
      - [注意事項](#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85-2)
    - [useSettings.js](#usesettingsjs)
      - [功能](#%E5%8A%9F%E8%83%BD-14)
      - [用法示例](#%E7%94%A8%E6%B3%95%E7%A4%BA%E4%BE%8B)
    - [<ins>useThrottle</ins>](#insusethrottleins)
      - [功能](#%E5%8A%9F%E8%83%BD-15)
      - [用法示例](#%E7%94%A8%E6%B3%95%E7%A4%BA%E4%BE%8B-1)
    - [<ins>useToggle</ins>](#insusetoggleins)
      - [功能](#%E5%8A%9F%E8%83%BD-16)
      - [用法示例](#%E7%94%A8%E6%B3%95%E7%A4%BA%E4%BE%8B-2)
    - [<ins>useTxnLog</ins>](#insusetxnlogins)
      - [`LogDTO` 日誌資料傳輸物件](#logdto-%E6%97%A5%E8%AA%8C%E8%B3%87%E6%96%99%E5%82%B3%E8%BC%B8%E7%89%A9%E4%BB%B6)
      - [`recordLog` 紀錄日誌函數](#recordlog-%E7%B4%80%E9%8C%84%E6%97%A5%E8%AA%8C%E5%87%BD%E6%95%B8)
      - [`fetchData`、`handleFetchError` 和 `fetchWrapper` 函數](#fetchdatahandlefetcherror-%E5%92%8C-fetchwrapper-%E5%87%BD%E6%95%B8)
      - [`useTxnLog` Hook](#usetxnlog-hook)
    - [<ins>useSCSBWebATM</ins>](#insusescsbwebatmins)
      - [同步和異步函數如何使用 ?](#%E5%90%8C%E6%AD%A5%E5%92%8C%E7%95%B0%E6%AD%A5%E5%87%BD%E6%95%B8%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8-)
      - [各功能介紹](#%E5%90%84%E5%8A%9F%E8%83%BD%E4%BB%8B%E7%B4%B9)
  - [<ins>共用 HOC</ins>](#ins%E5%85%B1%E7%94%A8-hocins)
    - [<ins>withKeyboard 高階元件</ins>](#inswithkeyboard-%E9%AB%98%E9%9A%8E%E5%85%83%E4%BB%B6ins)
    - [<ins>withLazyLoading 高階元件</ins>](#inswithlazyloading-%E9%AB%98%E9%9A%8E%E5%85%83%E4%BB%B6ins)
      - [使用方式](#%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F-1)
      - [參數](#%E5%8F%83%E6%95%B8)
      - [如何工作](#%E5%A6%82%E4%BD%95%E5%B7%A5%E4%BD%9C)
      - [範例](#%E7%AF%84%E4%BE%8B-29)
    - [<ins>withLoadable 高階元件</ins>](#inswithloadable-%E9%AB%98%E9%9A%8E%E5%85%83%E4%BB%B6ins)
      - [使用方式](#%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F-2)
      - [屬性](#%E5%B1%AC%E6%80%A7-1)
      - [全版面遮罩式載入特效](#%E5%85%A8%E7%89%88%E9%9D%A2%E9%81%AE%E7%BD%A9%E5%BC%8F%E8%BC%89%E5%85%A5%E7%89%B9%E6%95%88)
      - [示例](#%E7%A4%BA%E4%BE%8B-1)
    - [<ins>withOverwriteProps 高階元件</ins>](#inswithoverwriteprops-%E9%AB%98%E9%9A%8E%E5%85%83%E4%BB%B6ins)
      - [使用方式](#%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F-3)
      - [函數簽名](#%E5%87%BD%E6%95%B8%E7%B0%BD%E5%90%8D)
      - [參數](#%E5%8F%83%E6%95%B8-1)
      - [附加新屬性](#%E9%99%84%E5%8A%A0%E6%96%B0%E5%B1%AC%E6%80%A7)
      - [示例](#%E7%A4%BA%E4%BE%8B-2)
    - [<ins>withTxnPageLoaded 高階元件</ins>](#inswithtxnpageloaded-%E9%AB%98%E9%9A%8E%E5%85%83%E4%BB%B6ins)
      - [使用方式](#%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F-4)
      - [函數簽名](#%E5%87%BD%E6%95%B8%E7%B0%BD%E5%90%8D-1)
      - [參數](#%E5%8F%83%E6%95%B8-2)
      - [功能和流程](#%E5%8A%9F%E8%83%BD%E5%92%8C%E6%B5%81%E7%A8%8B)
      - [示例](#%E7%A4%BA%E4%BE%8B-3)
    - [<ins>withTxnPageLoaded 高階元件</ins>](#inswithtxnpageloaded-%E9%AB%98%E9%9A%8E%E5%85%83%E4%BB%B6ins-1)
      - [使用方式](#%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F-5)
      - [函數簽名](#%E5%87%BD%E6%95%B8%E7%B0%BD%E5%90%8D-2)
      - [參數](#%E5%8F%83%E6%95%B8-3)
      - [功能和流程](#%E5%8A%9F%E8%83%BD%E5%92%8C%E6%B5%81%E7%A8%8B-1)
      - [示例](#%E7%A4%BA%E4%BE%8B-4)
    - [<ins>withWrappedByDiv 高階元件</ins>](#inswithwrappedbydiv-%E9%AB%98%E9%9A%8E%E5%85%83%E4%BB%B6ins)
      - [使用方式](#%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F-6)
      - [函數簽名](#%E5%87%BD%E6%95%B8%E7%B0%BD%E5%90%8D-3)
      - [參數](#%E5%8F%83%E6%95%B8-4)
      - [功能](#%E5%8A%9F%E8%83%BD-17)
      - [示例](#%E7%A4%BA%E4%BE%8B-5)

<div style='page-break-before: always; height: 0; width: 0;'></div>

# [<ins>共用</ins>](#%E7%9B%AE%E6%AC%A1)

在專案中有個存放主要開發環境的檔案資料夾( src )，

而在其中有個 common 目錄，。

![](images/9XJR2Vg.png)

不論組件、工具、路由，只要有多個檔案共用都會分門別類放在 src/common 目錄下。

<br />

## [<ins>共用組件</ins>](#%E7%9B%AE%E6%AC%A1)

共用組件位於 src/common/components 目錄下，打開會看到類似以下的結構。

![](images/mo9aPJ4.png)

> 衍生組件命名格式為: [狀態名稱][組件名稱].jsx。
>
> 如果看到資料夾結構的組件，內部有多個名稱為以上格式，則代表為衍生組件，用意是為了方便開發，節省程式碼設定。
>
> 除了 PropTypes 和 DefaultProps 以外，組件有按照 `JSDoc` 註釋，
> 敘說參數以及用法
> 
> 這邊要保持一個觀念，假如只使用單個組件就請只引入單個組件，而不要採取引入整個組件資料夾的作法。

<br />

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>錯誤訊息(ErrorMsg)</ins>](#%E7%9B%AE%E6%AC%A1)

`ErrorMsg` 組件是一個 React 組件，用於顯示警告或錯誤訊息。它接受一條訊息文本和一個可選的 HTML 元素標籤作為屬性，用於自定義訊息的外觀。

#### 屬性（Props）

| 屬性     | 描述                                                   |
| -------- | ------------------------------------------------------ |
| `msg`    | 要顯示的警告或錯誤訊息文本。                           |
| `tag`    | 要渲染的 HTML 元素標籤，用於包裹訊息文本，默認為 'div'。 |

#### 範例

```javascript
import React from 'react';
import ErrorMsg from './ErrorMsg';

const MyComponent = () => {
  return (
    <div>
      <input type="text" />
      <ErrorMsg msg="這是一條錯誤訊息" tag="span" />
    </div>
  );
};

export default MyComponent;
```

在上述範例中，`ErrorMsg` 組件用於顯示一條錯誤訊息，它將訊息文本包裝在 `<span>` 元素中，以便自定義樣式。您可以根據需要將其用於表單驗證或其他需要顯示錯誤訊息的情境。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>標籤(Label)</ins>](#%E7%9B%AE%E6%AC%A1)

> 這是一個用於建立標籤的可重複使用 React 元件。

#### 屬性 (Props)

| 屬性名稱 | 類型 | 描述 |
| -------- | ---- | ---- |
| `htmlFor` | 字串 | 對應的 `for` 屬性。 |
| `required` | 布林值 | 是否顯示必填符號。 |
| `warn` | 布林值 | 是否顯示警告樣式。 |
| `text` | 字串 (必需) | 顯示的文字。 |
| `colMd3` | 布林值 | 是否啟用 `col-md-3` 樣式。 |
| `className` | 字串 | 自訂替換樣式。 |
| `attachClassName` | 字串陣列 | 要附加的樣式字串陣列。 |

#### 預設屬性 (Default Props)

| 屬性名稱 | 預設值 | 描述 |
| -------- | ------- | ---- |
| `htmlFor` | `''` | 對應的 `for` 屬性。 |
| `required` | `false` | 是否顯示必填符號。 |
| `attachClassName` | `[]` | 附加的樣式字串陣列。 |

#### 範例

```jsx
<Label 
    text='標籤文字' 
    attachClassName={['附加樣式標籤1']} 
    required 
/>
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>表單(Form)</ins>](#%E7%9B%AE%E6%AC%A1)

`Form` 是一個 React 組件，用於呈現 HTML 表單，同時提供禁用 HTML5 表單驗證的功能。它接受子組件和一個自訂的提交事件處理函數。

#### 屬性（Props）

| 屬性           | 描述                                                   |
| -------------- | ------------------------------------------------------ |
| `children`     | 表單內容的子組件。可以包含表單元素、按鈕等。            |
| `onSubmit`     | 自訂的表單提交事件處理函數。它會在表單提交時觸發，可用於執行自訂的表單驗證或處理邏輯。     |

#### 功能

- `Form` 組件呈現一個包含所有子組件的 HTML 表單。
- 透過將 `noValidate` 屬性設置為 `true`，`Form` 組件禁用了 HTML5 表單驗證，這表示不會出現預設的瀏覽器驗證提示或行為。
- `Form` 組件接受子組件，你可以在其中放置任何表單元素，例如輸入字段、按鈕等。
- 透過將自訂的 `onSubmit` 事件處理函數傳遞給 `Form` 組件，你可以在表單提交時執行自訂的邏輯。在範例中，`onSubmit` 函數阻止了預設的表單提交行為，你可以根據需要在其中添加表單驗證邏輯。

#### 範例

```javascript
import React from 'react';
import Form from './Form';

const MyForm = () => {
  const handleSubmit = (e) => {
    e.preventDefault();
    // 在此處處理表單提交事件，例如表單驗證和資料提交
  };

  return (
    <Form onSubmit={handleSubmit}>
      <input type="text" name="username" placeholder="使用者名稱" />
      <input type="password" name="password" placeholder="密碼" />
      <button type="submit">提交</button>
    </Form>
  );
};

export default MyForm;
```

在上述範例中，`Form` 組件包含輸入字段和提交按鈕，同時禁用了瀏覽器的 HTML5 表單驗證。在表單提交時，自訂的 `處理提交` 函數將被呼叫，你可以在其中執行表單驗證和資料提交等操作。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>輸入框(inputs)</ins>](#%E7%9B%AE%E6%AC%A1)

>`inputs` 為組件資料夾結構。

#### Input 元件

> 這是一個可重複使用的 React 元件，用於創建輸入框。

##### 屬性 (Props)

| 屬性名稱 | 類型 | 描述 |
| -------- | ---- | ---- |
| `disabled` | 布林值 | 是否禁用輸入框。 |
| `id` | 字串 (必需) | 對應的 `id` 屬性。 |
| `name` | 字串 | 對應的 `name` 屬性。 |
| `placeholder` | 字串 | 佔位符。 |
| `floatLabel` | 字串 | 出現在輸入框內的標籤。 |
| `type` | 字串 | 輸入框類型，可選值有 TEXT / PWD / EMAIL。 |
| `value` | 字串 | 輸入框的值。 |
| `onChange` | 函數 (必需) | 變換事件的處理函數。 |
| `errorMsg` | 字串 | 警示訊息。 |
| `inputStyle` | 物件 | 內聯樣式。 |
| `className` | 字串 | 自定義替換樣式。 |
| `autocomplete` | 字串 | 對應的自動完成屬性。 |
| `isVaild` | 布林值 | 是否顯示綠色框框樣式（用於驗證成功時顯示）。 |
| `floatMsg` | 布林值 | 是否將 errorMsg 樣式設定為 true：出現在輸入框上方，false：出現在輸入框下方。 |
| `isWrappedWithFloatingCustomWrapper` | 布林值 | 是否包含上層 div 樣式。 |
| `maxLength` | 字串 | 輸入框的最大長度。 |
| `isHasDefaultCn` | 布林值 | 是否擁有預設的 classname，預設為擁有。 |
| `keyBoard` | 元素 | 小鍵盤元件。 |

##### 預設屬性 (Default Props)

| 屬性名稱 | 預設值 | 描述 |
| -------- | ------- | ---- |
| `autocomplete` | `'off'` | 自動完成屬性。 |
| `floatMsg` | `false` | 是否將 errorMsg 樣式設定為 true：出現在輸入框上方，false：出現在輸入框下方。 |
| `isWrappedWithFloatingCustomWrapper` | `true` | 是否包含上層 div 樣式。 |
| `isHasDefaultCn` | `true` | 是否擁有預設的 classname。 |

##### 範例

```jsx
<Input
  id='userInput'
  type={INPUT_TYPE.TEXT}
  value={state.value}
  onChange={handleChange}
  floatLabel='使用者代號' // 會出現在輸入框內的標籤
/>

<Input
  id='userInput'
  type={INPUT_TYPE.TEXT}
  value={state.value}
  errorMsg={state.errorMsg}
  floatMsg   // true: 檢視訊息出現在輸入框上方，false: 檢視訊息出現在輸入框下方
  onChange={handleChange}
/>

<Input
  id='userInput'
  type={INPUT_TYPE.TEXT}
  value={state.value}
  onChange={handleChange}
/>
<ErrorMsg msg={state.errorMsg} />
```

#### PwdInput 元件

`PwdInput` 是一個預先設定為密碼 (password) 類型的輸入組件，可用於收集密碼輸入。

##### 屬性 (Props)

`PwdInput` 繼承自 `Input` 元件，因此具有與 `Input` 相同的屬性，這些屬性包括：

| 屬性名稱        | 類型     | 描述                          |
| --------------- | -------- | ----------------------------- |
| `disabled`      | 布林值   | 是否禁用輸入框。             |
| `id`            | 字串 (必需) | 對應的 `id` 屬性。            |
| `name`          | 字串     | 對應的 `name` 屬性。          |
| `placeholder`   | 字串     | 佔位符。                    |
| `value`         | 字串     | 輸入框的值。                  |
| `onChange`      | 函數 (必需) | 變換事件的處理函數。         |
| `errorMsg`      | 字串     | 警示訊息。                    |
| `inputStyle`    | 物件     | 內聯樣式。                    |
| `className`     | 字串     | 自定義替換樣式。             |
| `autocomplete`  | 字串     | 對應的自動完成屬性。           |
| `isVaild`       | 布林值   | 是否顯示綠色框框樣式（用於驗證成功時顯示）。 |
| `floatMsg`      | 布林值   | 是否將 errorMsg 樣式設定為 true：出現在輸入框上方，false：出現在輸入框下方。 |
| `isWrappedWithFloatingCustomWrapper`      | 布林值   | 是否包含上層 div 樣式。      |
| `maxLength`     | 字串     | 輸入框的最大長度。           |
| `isHasDefaultCn` | 布林值 | 是否擁有預設的 classname，預設為擁有。 |
| `keyBoard`      | 元素     | 小鍵盤元件。                 |

##### 範例

###### 基本用法

```jsx
<PwdInput
  id='userPwd'
  value={state.value}
  onChange={handleChange}
/>
```

###### 檢核訊息提示 (自身)

```jsx
<PwdInput
  id='userPwd'
  value={state.value}
  errorMsg={state.errorMsg}
  onChange={handleChange}
/>
```

###### 檢核訊息提示 (外部組件)

```jsx
<PwdInput
  id='userPwd'
  value={state.value}
  onChange={handleChange}
/>
<ErrorMsg msg={state.errorMsg} />
```

#### TextInput 元件

`TextInput` 是一個預先設定為文本 (text) 類型的輸入組件，可用於收集文本輸入。

##### 屬性 (Props)

`TextInput` 繼承自 `Input` 元件，因此具有與 `Input` 相同的屬性，這些屬性包括：

| 屬性名稱        | 類型     | 描述                          |
| --------------- | -------- | ----------------------------- |
| `disabled`      | 布林值   | 是否禁用輸入框。             |
| `id`            | 字串 (必需) | 對應的 `id` 屬性。            |
| `name`          | 字串     | 對應的 `name` 屬性。          |
| `placeholder`   | 字串     | 佔位符。                    |
| `value`         | 字串     | 輸入框的值。                  |
| `onChange`      | 函數 (必需) | 變換事件的處理函數。         |
| `errorMsg`      | 字串     | 警示訊息。                    |
| `inputStyle`    | 物件     | 內聯樣式。                    |
| `className`     | 字串     | 自定義替換樣式。             |
| `autocomplete`  | 字串     | 對應的自動完成屬性。           |
| `isVaild`       | 布林值   | 是否顯示綠色框框樣式（用於驗證成功時顯示）。 |
| `floatMsg`      | 布林值   | 是否將 errorMsg 樣式設定為 true：出現在輸入框上方，false：出現在輸入框下方。 |
| `isWrappedWithFloatingCustomWrapper`      | 布林值   | 是否包含上層 div 樣式。      |
| `maxLength`     | 字串     | 輸入框的最大長度。           |
| `isHasDefaultCn` | 布林值 | 是否擁有預設的 classname，預設為擁有。 |
| `keyBoard`      | 元素     | 小鍵盤元件。                 |

##### 範例

###### 基本用法

```jsx
<TextInput
  id='userText'
  value={state.value}
  onChange={handleChange}
/>
```

###### 檢核訊息提示 (自身)

```jsx
<TextInput
  id='userText'
  value={state.value}
  errorMsg={state.errorMsg}
  onChange={handleChange}
/>
```

###### 檢核訊息提示 (外部組件)

```jsx
<TextInput
  id='userText'
  value={state.value}
  onChange={handleChange}
/>
<ErrorMsg msg={state.errorMsg} />
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>單選框(Radio)</ins>](#%E7%9B%AE%E6%AC%A1)

`Radio` 是一個單選框元件，用於在表單中選擇單一選項。它可以簡單地單獨使用，也可以與其他單選框組合成一個單選框群組。

#### 屬性 (Props)

##### 單選框 (Radio)

| 屬性名稱            | 類型       | 描述                               |
| ------------------- | ---------- | ---------------------------------- |
| `id`                | 字串 (必需) | 對應的 `id` 屬性。                   |
| `name`              | 字串     | 對應的 `name` 屬性。                 |
| `value`             | 字串 (必需) | 單選框的值。                          |
| `labelText`         | 字串     | 標籤文字。                          |
| `checked`           | 布林值     | 是否默認選中單選框。                  |
| `disabled`          | 布林值     | 是否禁用單選框。                      |
| `onChange`          | 函數     | 當選項改變時觸發的事件處理函數。      |
| `inputCn`           | 字串     | 單選框的 class name 屬性。             |
| `labelCn`           | 字串     | 標籤的 class name 屬性。               |
| `isFormCheck`       | 布林值     | 是否自動包裹在 `FormCheckWrapper` 元件中。 |
| `child`             | 元素     | 顯示在文字後方的子元件。                |
| `attachWrapClassName` | 字串陣列 | 附加到 `FormCheckWrapper` 元件的 class name 字串陣列。 |

##### 單選框群組 (Radio.Group)

| 屬性名稱            | 類型       | 描述                               |
| ------------------- | ---------- | ---------------------------------- |
| `name`              | 字串     | 所有單選框的相同 `name` 屬性，用於將它們分組在一起。 |
| `disabled`          | 布林值     | 是否禁用整個單選框群組，可覆蓋個別單選框的 `disabled` 屬性。 |
| `whoChecked`        | 字串陣列   | 預設選中的單選框值，以字串陣列形式指定。   |
| `onChange`          | 函數     | 當選擇改變時觸發的事件處理函數，可覆蓋個別單選框的 `onChange` 屬性。 |
| `options`           | 物件陣列   | 單選框選項的配置物件陣列，每個物件都包含以下屬性： |

<div style='page-break-before: always; height: 0; width: 0;'></div>

##### 單選框特殊樣式群組 (Radio.BtnGroup)

`Radio.BtnGroup` 具有與 `Radio.Group` 相同的屬性，但它專為特殊樣式的單選框群組而設計。

#### 範例

##### 單獨使用單選框

```jsx
<Radio
  name='radioOptions'
  id='radio1'
  value='option1'
  labelText='選項 1'
  onChange={handleChange}
/>
```

##### 單選框群組

```jsx
<Radio.Group
  name='radioOptions'
  whoChecked={['option2']}
  options={[
    {
      id: 'radio1',
      value: 'option1',
      labelText: '選項 1',
      onChange: handleChange
    },
    {
      id: 'radio2',
      value: 'option2',
      labelText: '選項 2',
      onChange: handleChange,
      checked: true
    },
    {
      id: 'radio3',
      value: 'option3',
      labelText: '選項 3',
      onChange: handleChange
    }
  ]}
/>
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

##### 特別樣式的單選框群組

```jsx
<Radio.BtnGroup
  name='radioOptions'
  whoChecked={['option2']}
  options={[
    {
      id: 'radio1',
      value: 'option1',
      labelText: '選項 1',
      onChange: handleChange
    },
    {
      id: 'radio2',
      value: 'option2',
      labelText: '選項 2',
      onChange: handleChange,
      checked: true
    },
    {
      id: 'radio3',
      value: 'option3',
      labelText: '選項 3',
      onChange: handleChange
    }
  ]}
/>
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>下拉選單(Dropdown)</ins>](#%E7%9B%AE%E6%AC%A1)

#### Dropdown 元件

`Dropdown` 元件是一個可重複使用的下拉選單組件，用於選擇一個選項。

##### 屬性 (Props)

`Dropdown` 元件具有以下屬性：

| 屬性名稱           | 類型         | 描述                                                  |
| ------------------ | ------------ | ----------------------------------------------------- |
| `id`               | 字串 (必需) | 下拉選單的唯一識別符。                                |
| `name`             | 字串         | 下拉選單的名稱。                                      |
| `value`            | 字串         | 下拉選單的當前值。                                    |
| `disabled`         | 布林值       | 是否禁用下拉選單。                                    |
| `warn`             | 布林值       | 是否啟動警告下拉元件屬性。                            |
| `onChange`         | 函數 (必需)  | 當選擇項目發生變化時觸發的回調函數。                |
| `options`          | 陣列         | 下拉選單中的選項列表。                                |
| `attachClassName`  | 陣列         | 要附加到下拉選單的自定義 CSS 類名的陣列。            |
| `defaultOption`    | 布林值       | 是否顯示預設選項。                                    |
| `defaultOptionText`| 字串         | 預設選項的文字。                                      |
| `spantext`         | 字串         | 預設 span 文字。                                      |

##### 範例

###### 基本用法

```jsx
<Dropdown
  id='dropdown'
  value={state.value}
  onChange={handleChange}
  options={[
    { title: '選項1', value: 'option1' },
    { title: '選項2', value: 'option2' }
  ]}
  defaultOption
/>
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

###### 自訂預設選項文字

```jsx
<Dropdown
  id='dropdown'
  value={state.value}
  onChange={handleChange}
  options={[
    { title: '選項1', value: 'option1' },
    { title: '選項2', value: 'option2' }
  ]}
  defaultOption
  defaultOptionText='請選擇'
/>
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

#### DropdownCustom(Dropdown.Custom) 元件

`DropdownCustom` 元件是一個客製化的下拉選單，支援多行選項，可用於選擇一個或多個選項。

##### 屬性 (Props)

`DropdownCustom` 具有以下屬性：

| 屬性名稱           | 類型         | 描述                                                  |
| ------------------ | ------------ | ----------------------------------------------------- |
| `id`               | 字串 (必需) | 下拉選單的唯一識別符。                                |
| `text`             | 任何 (必需) | 預設顯示在按鈕上的文字或 React 元素。              |
| `name`             | 字串         | 下拉選單的名稱。                                      |
| `value`            | 字串         | 下拉選單的當前值。                                    |
| `msg`              | 字串         | 顯示的訊息。                                          |
| `disabled`         | 布林值       | 是否禁用下拉選單。                                    |
| `onChange`         | 函數 (必需)  | 當選擇項目發生變化時的回調函數。                      |
| `warn`             | 布林值       | 是否顯示警告。                                        |
| `spantext`         | 字串         | 額外的文字標籤。                                      |
| `btnAttachClassName`| 陣列        | 附加在按鈕上的自定義 CSS 類名的陣列。                |
| `options`          | 陣列         | 下拉選單中的選項列表。                                |
| `linkOption`       | 物件         | 連結選項物件，包含連結的文字和 URL。                 |
| `custDropdownCn`   | 字串         | 自訂下拉選單的 CSS 類名。                             |

##### 範例

###### 基本用法

```jsx
<DropdownCustom
  id='dropdownCustom'
  text='選擇項目'
  onChange={handleDropdownChange}
  options={[
    {
      display: '選項 1',
      disabled: false,
      leftArea: {
        title: '標題 1',
        values: ['值 1']
      },
      rightArea: {
        title: '標題 2',
        values: ['值 2']
      }
    },
    {
      display: '選項 2',
      disabled: true,
      leftArea: {
        title: '標題 3',
        values: ['值 3', '值 4']
      },
      rightArea: {
        title: '標題 4',
        values: ['值 5', '值 6']
      }
    }
  ]}
/>
```

###### 自訂預設文字

```jsx
<DropdownCustom
  id='dropdownCustom'
  text='自訂文字'
  onChange={handleDropdownChange}
  options={[
    {
      display: '選項 1',
      disabled: false,
      leftArea: {
        title: '標題 1',
        values: ['值 1']
      },
      rightArea: {
        title: '標題 2',
        values: ['值 2']
      }
    },
    {
      display: '選項 2',
      disabled: true,
      leftArea: {
        title: '標題 3',
        values: ['值 3', '值 4']
      },
      rightArea: {
        title: '標題 4',
        values: ['值 5', '值 6']
      }
    }
  ]}
/>
```

#### DropDownCustomMenu(Dropdown.CustomMenu) 元件

`DropDownCustomMenu` 元件是一個客製化的下拉選單，支援搜尋功能，搜尋框位於選項中，用戶可以根據搜尋文字篩選選項。

##### 屬性 (Props)

`DropDownCustomMenu` 具有以下屬性：

| 屬性名稱           | 類型         | 描述                                                  |
| ------------------ | ------------ | ----------------------------------------------------- |
| `id`               | 字串 (必需) | 下拉選單的唯一識別符。                                |
| `text`             | 字串 (必需) | 按鈕上顯示的文字。                                    |
| `searchPlaceholder`| 字串         | 搜尋框的提示文字。                                    |
| `searchText`       | 字串         | 預設搜尋文字。                                        |
| `name`             | 字串         | 下拉選單的名稱。                                      |
| `value`            | 字串         | 下拉選單的當前值。                                    |
| `msg`              | 字串         | 顯示的訊息。                                          |
| `disabled`         | 布林值       | 是否禁用下拉選單。                                    |
| `onChange`         | 函數 (必需)  | 當選擇項目發生變化時的回調函數。                      |
| `options`          | 陣列         | 下拉選單中的選項列表。                                |
| `warn`             | 布林值       | 是否顯示警告。                                        |
| `linkOption`       | 物件         | 連結選項物件，包含連結的文字和 URL。                 |
| `spantext`         | 字串         | 額外的文字標籤。                                      |
| `custDropdownCn`   | 字串         | 自訂下拉選單的 CSS 類名。                             |

##### 範例

###### 基本用法

```jsx
<DropDownCustomMenu
  id='dropdownCustomMenu'
  text='選擇項目'
  searchPlaceholder='搜尋選項'
  onChange={handleDropdownChange}
  options={[
    {
      title: '選項 1',
      value: '值 1',
      content: <div>自定義內容 1</div>,
      classname: 'custom-class-1'
    },
    {
      title: '選項 2',
      value: '值 2',
      content: <div>自定義內容 2</div>,
      classname: 'custom-class-2'
    }
  ]}
/>
```

###### 自訂預設文字和搜尋文字

```jsx
<DropDownCustomMenu
  id='dropdownCustomMenu'
  text='自訂文字'
  searchPlaceholder='自訂搜尋文字'
  searchText='搜尋預設文字'
  onChange={handleDropdownChange}
  options={[
    {
      title: '選項 1',
      value: '值 1',
      content: <div>自定義內容 1</div>,
      classname: 'custom-class-1'
    },
    {
      title: '選項 2',
      value: '值 2',
      content: <div>自定義內容 2</div>,
      classname: 'custom-class-2'
    }
  ]}
/>
```

以下是有關`DropDownCustomSearch`元件的介紹：

#### DropDownCustomSearch(Dropdown.CustomSearch) 元件

`DropDownCustomSearch` 元件是一個客製化的下拉選單，具有搜尋功能，且搜尋框與按鈕位於同一層，用戶可以根據搜尋文字篩選選項。

##### 屬性 (Props)

`DropDownCustomSearch` 具有以下屬性：

| 屬性名稱           | 類型         | 描述                                                  |
| ------------------ | ------------ | ----------------------------------------------------- |
| `options`          | 陣列 (必需) | 選項數組，每個選項是一個物件。                        |
| `onSelect`         | 函數 (必需)  | 當選擇項目時的回調函數，清除時也會觸發。              |
| `placeholder`      | 字串         | 輸入框的占位符。                                      |
| `disabled`         | 布林值       | 是否禁用下拉搜尋框。                                  |
| `isDisabledAndClear` | 布林值     | 是否禁用下拉搜尋框，並同時清除輸入框。                |

##### 自定義選項物件 (options)

`options` 屬性是一個陣列，每個元素代表一個下拉選項，並具有以下屬性：

- `title` (必需): 選項的標題。
- `fundType`: 選項的基金類型。
- `render`: 自定義渲染內容的函數，如果提供，將使用自定義渲染，否則使用預設渲染。
- `value` (必需): 選項的值。
- `disabled`: 是否禁用選項。
- `className`: 自訂的 CSS 類名。
- `onClick`: 當選項被點擊時的回呼函數，將以選項的值作為參數進行調用。

##### 範例

###### 基本用法

```jsx
<DropDownCustomSearch
  placeholder='請輸入產品關鍵字或 4 碼代碼'
  onSelect={(val) => console.log('onSelect', val)}
  options={[
    {
      title: '摩根投信 一 1401 摩根台灣增長',
      fundType: '穩健型',
      value: '1401'
    },
    {
      title: 'TWD  1402 摩根新興科技基金',
      fundType: '穩健型',
      value: '1402'
    },
    {
      title: 'JPY  1407 摩根新興日本基金',
      fundType: '積極型',
      value: '1407',
      disabled: true
    }
  ]}
/>
```

###### 使用自定義選項結構

```jsx
<DropDownCustomSearch
  placeholder='請輸入產品關鍵字或 4 碼代碼'
  onSelect={(val) => console.log('onSelect', val)}
  options={[
    {
      title: '摩根投信 一 1401 摩根台灣增長',
      fundType: '穩健型',
      value: '1401',
      render: (
        <>
          <span>摩根投信 一 1401 摩根台灣增長</span>
          <span className='fundType'>穩健型</span>
        </>
      )
    },
    {
      title: 'TWD  1402 摩根新興科技基金',
      fundType: '穩健型',
      value: '1402',
      render: (
        <>
          <span>TWD  1402 摩根新興科技基金</span>
          <span className='fundType'>穩健型</span>
        </>
      )
    },
    {
      title: 'JPY  1407 摩根新興日本基金',
      fundType: '積極型',
      value: '1407',
      disabled: true,
      render: (
        <>
          <span>JPY  1407 摩根新興日本基金</span>
          <span className='fundType'>積極型</span>
        </>
      )
    }
  ]}
/>
```

這個`DropDownCustomSearch`元件允許創建可自定義的下拉選單，用戶可以使用搜尋框篩選選項，並在選擇項目時觸發回調函數。同時可以使用自定義的選項結構以滿足特定的需求。

以下是有關 `DropdownCurrency` 元件的介紹：

#### DropdownCurrency(Dropdown.Currency) 元件

`DropdownCurrency` 元件是一個用於下拉選擇貨幣的自訂組件，允許用戶在可用的貨幣之間進行選擇。此元件支援多個常見的貨幣代碼，並可進行自定義配置。

##### 屬性 (Props)

`DropdownCurrency` 具有以下屬性：

| 屬性名稱           | 類型         | 描述                                                  |
| ------------------ | ------------ | ----------------------------------------------------- |
| `currencies`       | 陣列/字串   | 允許的貨幣代碼，可以是陣列或字串。預設為 `TWD` (新台幣)。 |
| `onChange`         | 函數         | 選擇貨幣變化時的回調函數，初始化時也會觸發。              |
| `value`            | 字串         | 當前選擇的貨幣代碼。                                    |

##### 貨幣選項 (currencies)

`currencies` 屬性指定允許的貨幣代碼。它可以是一個字串（例如，`'TWD'`）或一個貨幣代碼的陣列（例如，`['TWD', 'USD']`）。您可以根據需要配置這些貨幣代碼。如果未指定，則預設為 `TWD`（新台幣）。

##### onChange 回調函數 (onChange)

`onChange` 屬性是一個函數，它將在選擇貨幣變化時被調用。該函數將接收當前選擇的貨幣代碼作為參數。這允許您在用戶選擇不同貨幣時執行相應的操作。

##### value 屬性

`value` 屬性用於指定初始選擇的貨幣代碼。如果指定了這個值，則在初始化時將選擇該貨幣代碼對應的貨幣選項。如果未指定，則使用 `currencies` 屬性的第一個貨幣選項作為初始選擇。

##### 範例

###### 基本用法

```jsx
<DropdownCurrency
  currencies={['TWD', 'USD']}
  onChange={(code) => {
    console.log('onChange', code);
  }}
/>
```

在此範例中，`DropdownCurrency` 元件允許用戶選擇 `TWD`（新台幣）和 `USD`（美元）中的一種貨幣。選擇變化時，`onChange` 回調函數將被觸發。

###### 使用全部貨幣選項

```jsx
<DropdownCurrency
  currencies='ALL'
  onChange={(code) => {
    console.log('onChange', code);
  }}
/>
```

在此範例中，`DropdownCurrency` 元件允許用戶從所有可用的貨幣選項中進行選擇。當用戶選擇不同的貨幣時，`onChange` 回調函數將被觸發。

###### 指定初始選擇的貨幣

```jsx
<DropdownCurrency
  value='USD'
  currencies='ALL'
  onChange={(code) => {
    console.log('onChange', code);
  }}
/>
```

在此範例中，`DropdownCurrency` 元件將初始選擇 `USD`（美元）作為預設選擇。當用戶選擇不同的貨幣時，`onChange` 回調函數將被觸發。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>日期元件(DatePicker)</ins>](#%E7%9B%AE%E6%AC%A1)

`DatePicker` 元件是一個用於選擇日期的自訂元件，它使用了 `react-datepicker` 庫，並提供了許多自定義選項，以便更好地適應您的需求。

#### 屬性 (Props)

`DatePicker` 具有以下屬性：

| 屬性名稱         | 類型       | 描述                                                               |
| ---------------- | ---------- | ------------------------------------------------------------------ |
| `dateFormat`     | 字串       | 畫面顯示日期的格式。預設為 `yyyy/MM/dd`。                            |
| `id`             | 字串       | 對應的 id 屬性。                                                    |
| `name`           | 字串       | 對應的 name 屬性。                                                  |
| `initValue`      | 字串       | 預設日期，需要傳入 `YYYYMMDD` 格式，僅用於設定預設值。                  |
| `className`      | 字串       | 自定義替換樣式的 CSS 類名。                                           |
| `disabled`       | 布林值     | 是否禁用日曆元件。                                                    |
| `getValue`       | 函數       | 取得回傳日期的回調函數，回傳日期格式為 `YYYYMMDD`。                     |
| `placeholder`    | 字串       | 提示文字，顯示在輸入框中。                                            |
| `keydisabled`    | 布林值     | 是否禁用輸入框。                                                      |
| `spantext`       | 字串       | 若傳入此值，自動加入前方的 span 提示文字。                                 |
| `hasWrap`        | 布林值     | 是否啟用 `FloatingCustomWrapper` 包裝器，預設為啟用。                      |
| `mb3`            | 布林值     | 是否啟用 `mb3` CSS 類名，預設為啟用。                                    |
| `mb2`            | 布林值     | 是否啟用 `mb2` CSS 類名。                                                |
| `minDate`        | 字串       | 最小日期，傳入 `YYYYMMDD` 格式。                                        |
| `maxDate`        | 字串       | 最大日期，傳入 `YYYYMMDD` 格式。                                        |

#### 範例

##### 基本用法

```jsx
<DatePicker 
  id='date1' 
  getValue={getDate} //回調函數，回傳 `YYYYMMDD` 格式日期
  keydisabled={true} //禁用打字框
  initValue='20230303' //可加可不加，預設日期，僅用來設定預設值
  spantext='查詢起日' //自動加入 span 訊息
/>
```

在此範例中，`DatePicker` 元件允許用戶選擇日期，並在用戶選擇日期後調用 `getDate` 回調函數，回傳 `YYYYMMDD` 格式的日期。輸入框被禁用以避免直接輸入日期。

```jsx
const getDate = useCallback((date) => {
    console.log(date); //format:YYYYMMDD
}, []);
```

##### 使用 prop 設定

```jsx
<DatePicker 
  id='date'
  name='date'
  placeholder='請輸入日期' //提示文字
  disabled={true} //禁用日曆元件
  getValue={getDate}
  minDate='20230601'
  maxDate='20230614'
/>
```

在此範例中，`DatePicker` 元件根據 prop 設定，設置了提示文字、禁用日曆元件、日期範圍限制（最小日期為 `20230601`，最大日期為 `20230614`）。當用戶選擇日期時，選擇的日期將調用 `getDate` 回調函數，並回傳 `YYYYMMDD` 格式的日期。

#### 自定義日期格式 (`dateFormat`)

`dateFormat` 屬性用於指定畫面上顯示日期的格式。您可以自定義日期的顯示方式，例如 `yyyy/MM/dd` 或 `dd/MM/yyyy`。如果未指定，則預設為 `yyyy/MM/dd`。

#### 預設值 (`initValue`)

`initValue` 屬性可用於設定日期選擇器的初始值。這個值應該以 `YYYYMMDD` 格式傳遞。如果未指定 `initValue`，則日期選擇器將不顯示初始值。

#### 最小日期和最大日期 (`minDate` 和 `maxDate`)

您可以使用 `minDate` 和 `maxDate` 屬性來設定日期選擇器的最小日期和最大日期。這兩個屬性都應該以 `YYYYMMDD` 格式傳遞。如果未指定 `minDate`，則日期選擇器將不限制最小日期。如果未指定 `maxDate`，則日期選擇器將不限制最大日期。

#### 自定義 CSS 類名 (`className`)

`className` 屬性允許自定義日期選擇器的外觀，通過添加自己的 CSS 類名。

#### 自定義提示文字 (`spantext`)

如果希望在輸入框前方顯示一個自定義提示文字，可以使用 `spantext` 屬性。這個文字將顯示在輸入框前方的 `span` 元素中。

#### 禁用日期選擇元件 (`disabled` 和 `keydisabled`)

`disabled` 屬性用於禁用整個日期選擇元件，使其不可用。如果設置為 `true`，則日期選擇元件將無法使用。`keydisabled` 屬性用於禁用輸入框，使其無法直接輸入日期。

#### 取得選擇的日期 (`getValue`)

`getValue` 屬性是一個回調函數，當用戶選擇日期時，它將被調用，並將選擇的日期以 `YYYYMMDD` 格式作為參數傳遞。

#### 自定義日期選擇的過濾函數 (`filterDate`)

`filterDate` 可以指定一個回調函數，該函數將在使用者嘗試選擇日期時被呼叫，並且根據邏輯來決定是否允許選擇特定日期。

以下是關於 `filterDate` 選項的一些常見用法和說明：

1. **使用示例**：

   ```jsx
   <DatePicker
     filterDate={(date) => {
       // 返回 true 表示允許選擇該日期，返回 false 表示禁止選擇
       // 在這裡編寫日期選擇過濾邏輯
     }}
   />
   ```

2. **回調函數**：`filterDate` 接受一個回調函數作為參數，該函數將在使用者嘗試選擇日期時被呼叫。回調函數將接收一個 `Date` 對象作為參數，表示使用者選擇的日期。

3. **返回值**：回調函數應該返回一個布爾值，`true` 表示允許選擇該日期，`false` 表示禁止選擇該日期。您可以根據您的自訂邏輯來決定是否允許選擇特定日期。

4. **應用場景**：`filterDate` 常常用於以下場景：

   - 限制特定日期範圍，例如禁止選擇過去的日期或將來的日期。
   - 根據業務需求禁止某些日期，例如特定的假期或不營業的日期。
   - 根據業務需求允許某些日期，例如特定的假期或營業的日期。
   - 根據其他日期的選擇來動態決定可選擇的日期，例如選擇某日期後，禁止選擇某日期之前的日期。

5. **注意事項**：在回調函數中，您可以訪問使用者選擇的日期，並根據需要進行驗證。如果回調函數返回 `true`，使用者將能夠選擇該日期。如果回調函數返回 `false`，使用者將無法選擇該日期。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>多選日期天數元件(DayPicker)</ins>](#%E7%9B%AE%E6%AC%A1)

DayPicker 組件是一個多選日期天數選擇工具，用於呈現一個日期選擇界面，讓用戶能夠選擇一個或多個日期。該組件提供了多種配置選項，以適應不同的日期選擇需求。

#### 屬性（Props）

DayPicker 組件支援以下屬性：

| 屬性              | 描述                                                                                                                                                  | 類型                   | 默認值       |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | -------------- |
| `id`              | 組件的唯一標識符，通常用於區分頁面上的多個 DayPicker 組件。                                                                                          | 字符串（String）        | 生成的 UUID   |
| `name`            | 組件的名稱，通常用於表單提交時識別該組件。                                                                                                          | 字符串（String）        | 未設置         |
| `placeholder`     | 在輸入框中顯示的佔位文本，用於提示用戶可以在此處選擇日期。                                                                                        | 字符串（String）        | 選擇日期     |
| `disabled`        | 是否禁用日期選擇器，如果禁用，用戶將無法與日期選擇器進行交互。                                                                                     | 布爾值（Boolean）        | `false`        |
| `getValue`        | 用於接收用戶選擇的日期的回調函數。當用戶進行日期選擇時，將觸發此回調函數，您可以在其中處理選定的日期。                                                 | 函數（Function）         | 必填          |
| `displayDays`     | 日曆中顯示的日期數量。您可以設置此屬性來控制在日曆中顯示多少天的日期。                                                                               | 數字（Number）         | 28             |
| `icon`            | 自定義圖示元素，通常用於添加額外的信息或樣式。您可以傳遞一個 React 元素作為圖示，以便顯示在日期選擇器旁邊。                                     | React 元素（Element）   | 未設置         |
| `isChargeDays`    | 是否顯示特定的扣款日期，這些日期為 [2, 6, 12, 16, 22, 26]。如果設置為 `true`，將忽略 `displayDays` 屬性。                                           | 布爾值（Boolean）        | `false`        |
| `order`           | 日期的排序方式，可以是 `ORDER_TYPE.ASC`（升序）或 `ORDER_TYPE.DESC`（降序）。如果設置，將按照指定順序排序選擇的日期。                     | 字符串（String）        | 未設置         |
| `defaultPickedDays` | 默認選中的日期，以一個數字數組的形式傳遞。例如，`[1, 2, 3]` 表示默認選中了前三天的日期。                                                           | 數組（Array）            | 未設置         |
| `spantext`        | 前方的提示文字，用於添加額外的信息，通常與自定義圖示一起使用。                                                                                          | 字符串（String）        | 未設置         |

#### 功能

- DayPicker 組件允許用戶選擇一個或多個日期，用戶可以單擊日期來選擇或取消選擇日期。
- 可以配置顯示的日期範圍，以適應不同的需求。
- 支持自定義圖示和

提示文字，用戶可以查看額外的信息。
- 提供日期的排序功能，用戶可以按升序或降序排列選擇的日期。

#### 範例

以下是 DayPicker 組件的一些使用示例：

```javascript
import React from 'react';
import DayPicker from './DayPicker';

// 基本用法
<DayPicker
  displayDays={30} // 設定小日曆呈現的日期，不傳入則預設為 28 天
  getValue={handleSelectDates}
/>

const handleSelectDates = (days) => {
  console.log(days);
};

// 呈現特定日期的日曆，只有 2, 6, 12, 16, 22, 26 這些日期
<DayPicker
  isChargeDays={true}
  getValue={handleSelectDates}
/>

// 呈現日期升冪或降冪排序
import { ORDER_TYPE } from './ORDER_TYPE';
<DayPicker
  displayDays={30} // 設定小日曆呈現的日期，不傳入則預設為 28 天
  getValue={handleSelectDates}
  order={ORDER_TYPE.ASC} // 根據 ORDER_TYPE 可以選擇升冪或降冪排序
/>

// 呈現預先選擇的日期與傳入 spantext
<DayPicker
  displayDays={30} // 設定小日曆呈現的日期，不傳入則預設為 28 天
  getValue={handleSelectDates}
  defaultPickedDays={[1, 2, 3]}
  spantext={'每月扣款日期'}
/>

// 加入客製化 icon
<DayPicker
  displayDays={30}
  getValue={() => { }}
  icon={
    <i
      className='bi bi-info-circle-fill float-R'
      data-bs-toggle='tooltip'
      data-bs-placement='top'
      data-bs-html='true'
      title='投資日可複選，如遇例假日則順延至次一營業日'
    />
  }
/>
```

這些示例演示了 DayPicker 組件的不同用法，包括基本用法、顯示特定日期、排序日期、預選日期以及添加自定義圖示和提示文字。您可以根據需要選擇適合您的項目。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>彈跳視窗元件(Modal)</ins>](#%E7%9B%AE%E6%AC%A1)

**Modal 元件** 是一個用於創建彈出式對話框（燈箱）的自訂元件。它通常用於顯示訊息、表單、圖像或其他內容，並允許用戶與其進行互動。

#### 屬性（Props）

以下是 Modal 元件的屬性：

| 屬性名稱             | 類型       | 描述                                                                 |
| ------------------ | ---------- | -------------------------------------------------------------------- |
| `id`               | 字串       | 對應的 id 屬性。                                                        |
| `isOpen`           | 布林值     | 控制 Modal 是否開啟（true 表示開啟，false 表示關閉）。                        |
| `title`            | 任意       | Modal 的標題，可以是文字或 React 組件。                                       |
| `subtitle`         | 任意       | Modal 的副標題，可以是文字或 React 組件。                                      |
| `msg`              | 字串       | 顯示在 Modal 主內容區域的文字提示，如果設定了此屬性，`children` 屬性將無效。            |
| `children`         | React 組件  | Modal 主內容區域的子組件，如果設定了 `msg` 屬性，此屬性將無效。                   |
| `className`        | 字串       | 自定義的 CSS 類名，用於修改 Modal 的樣式。                                     |
| `onCloseBtn`       | 布林值     | 是否顯示關閉按鈕，true 表示顯示，false 表示隱藏。                                |
| `onClose`          | 函數       | 關閉 Modal 的回調函數。                                                    |
| `customContent`    | 任意       | 自訂 Modal 底部的內容，可以是文字或 React 組件。                                |
| `upperRightCloseBtn` | 布林值   | 是否顯示右上角的關閉按鈕，true 表示顯示，false 表示隱藏。                           |
| `backdropStatic`   | 布林值     | 點擊背景時是否關閉 Modal，true 表示不關閉，false 表示關閉。                          |
| `htmlContent`      | 字串       | 要渲染為 HTML 的內容字符串，如果設定了此屬性，`children` 和 `msg` 屬性將無效。         |
| `attachClassName`  | 字串陣列   | 要附加的 Modal 大小樣式字串陣列。                                              |

#### 範例

```jsx
import Modal from './Modal';

// 燈箱開啟
const [msg, setMsg] = useState(); // 燈箱中 body 裡面的內容
const [open, setOpen] = useState(false); // 開啟燈箱接口

<Modal
  id='customModal'
  isOpen={open}  // 控制 Modal 開啟關閉接口
  title='Custom Modal' // 放置於 Modal 標題，可傳入文字或組件
  msg={msg}  // 放置於 Modal Body，可傳入文字
  size={60}  // 若未設定則預設基本大小
  onCloseBtn  // 若標註會出現關閉按鈕，沒有標註則不會出現
  onClose={closeModal}  // 回調函數
/>
```

<div style='page-break-before: always; height: 0; width: 0;'></div>
 
### [<ins>虛擬鍵盤(KeyBoard)</ins>](#%E7%9B%AE%E6%AC%A1)

`Keyboard` 是一個 React 組件，用於在 Web 應用程序中添加虛擬鍵盤功能，使用戶可以進行虛擬鍵盤輸入。該組件提供兩種不同的小鍵盤：全功能小鍵盤（包括英文和數字）和數字小鍵盤。

#### 屬性 (Props)

`Keyboard` 組件具有以下屬性：

| 屬性名稱         | 類型     | 描述                                                                                       |
| ---------------- | -------- | ------------------------------------------------------------------------------------------ |
| `firstInputId`   | 字串     | 對應的輸入元素的 ID，當使用者點擊小鍵盤按鈕時，這個 ID 用於將輸入的字符插入到相應的輸入框中。 |

#### 全功能小鍵盤 (Full Keyboard)

`Full` 組件是一個包含全功能小鍵盤的組件，用於提供英文和數字字符的虛擬鍵盤。

```jsx
import Keyboard from './Keyboard';

<Keyboard.Full firstInputId="inputFieldId" />
```

#### 數字小鍵盤 (Numeric Keyboard)

`Numeric` 組件是一個僅包含數字字符的小鍵盤組件。

```jsx
import Keyboard from './Keyboard';

<Keyboard.Numeric firstInputId="numericInputFieldId" />
```

#### 使用 `withKeyboard` 高階組件 (HOC)

要在頁面組件中使用 `Keyboard` 組件，可以使用 `withKeyboard` 高階組件（HOC）。以下是如何使用 `withKeyboard` HOC 的示例：

```jsx
import React, { useRef, useEffect } from 'react';
import Keyboard from './Keyboard';

const YourPageComponent = ({ firstInputId }) => {
  const inputRef = useRef(null);

  useEffect(() => {
    // 使用 inputRef 監聽輸入框
  }, []);

  return (
    <div>
      {/* 將 Keyboard 組件包裝在 withKeyboard HOC 中 */}
      <Keyboard.Full firstInputId={firstInputId} />

      <input ref={inputRef} type="text" id={firstInputId} />
    </div>
  );
};

// 使用 withKeyboard 包裝您的頁面組件
export default withKeyboard(YourPageComponent);
```

請注意，`withKeyboard` HOC 接受一個名為 `firstInputId` 的屬性，並將其傳遞給 `Keyboard` 組件，以確保鍵盤輸入能夠與正確的輸入框關聯。

<div style='page-break-before: always; height: 0; width: 0;'></div>
 
### [<ins>泡泡框提示文字(tooltips)</ins>](#%E7%9B%AE%E6%AC%A1)

> `tooltips` 為組件資料夾結構。

#### Tooltip 泡泡提示框

`Tooltip` 組件用於在 Web 應用程序中添加泡泡提示框，通常用於提供有關特定元素的附加信息。

##### 屬性 (Props)

`Tooltip` 組件具有以下屬性：

| 屬性名稱          | 類型               | 描述                                                                                   |
| ------------------ | ------------------ | -------------------------------------------------------------------------------------- |
| `children`         | React 元素         | 子組件，會放在泡泡框左邊，優先度最高。                                              |
| `label`            | 字串或函數         | 泡泡框左邊文字，會放在泡泡框左邊，優先度低於子組件。接受字串或自定義渲染函數。   |
| `title`            | 字串               | 泡泡框顯示標題。                                                                       |
| `text`             | 字串或字串陣列     | 泡泡框顯示內文，可以是字串或字串陣列，支援換行。                                     |
| `state`            | 字串               | 泡泡框的位置，使用 `TOOLTIP_TYPE` 常數來取得上下左右的位置。                         |
| `smallWrap`        | 布林值             | 是否使用 `small` 元素包裹。                                                           |
| `className`        | 字串               | 自定義 class 樣式。                                                                    |
| `attachClassName`  | 字串陣列           | 自定義附加 class 樣式陣列。                                                            |

##### 使用示例

以下是如何使用 `Tooltip` 組件的示例：

基本用法：

```jsx
import Tooltip, { TOOLTIP_TYPE } from './Tooltip';

<Tooltip
  title='使用者代號(6-12位)'
  text='使用者代號請留意英文字母大小寫。若您是使用密碼通知書辦理簽入者，請輸入該密碼通知書序號。'
  state={TOOLTIP_TYPE.TOP}
/>
```

使用子組件：

```jsx
import Tooltip, { TOOLTIP_TYPE } from './Tooltip';
import Keyboard from './Keyboard';

<Tooltip
  title='使用者代號(6-12位)'
  text='使用者代號請留意英文字母大小寫。若您是使用密碼通知書辦理簽入者，請輸入該密碼通知書序號。'
  state={TOOLTIP_TYPE.TOP}
>
  <Keyboard foucsID='userText' onChange={handleChange} />
</Tooltip>
```

支援換行，可使用 `<br>` 或字串陣列：

```jsx
import Tooltip, { TOOLTIP_TYPE } from './Tooltip';

<Tooltip
  title='使用者代號(6-12位)'
  text={[
    '使用者代號請留意英文字母大小寫。',
    '若您是使用密碼通知書辦理簽入者，請輸入該密碼通知書序號。'
  ]}
  state={TOOLTIP_TYPE.TOP}
/>
```

#### 衍生組件

`Tooltip` 組件有幾個衍生組件，分別用於不同的泡泡框位置：

##### BottomTooltip

`BottomTooltip` 組件用於在底部顯示泡泡框。

```jsx
import BottomTooltip from './BottomTooltip';

<BottomTooltip
  title='使用者代號(6-12位)'
  text='使用者代號請留意英文字母大小寫。若您是使用密碼通知書辦理簽入者，請輸入該密碼通知書序號。'
  placehoder='忘記使用者代號' //在提示框旁邊的文字
/>
```

##### LeftTooltip

`LeftTooltip` 組件用於在左側顯示泡泡框。

```jsx
import LeftTooltip from './LeftTooltip';

<LeftTooltip
  title='使用者代號(6-12位)'
  text='使用者代號請留意英文字母大小寫。若您是使用密碼通知書辦理簽入者，請輸入該密碼通知書序號。'
  placehoder='忘記使用者代號' //在提示框旁邊的文字
/>
```

##### RightTooltip

`RightTooltip` 組件用於在右側顯示泡泡框。

```jsx
import RightTooltip from './RightTooltip';

<RightTooltip
  title='使用者代號(6-12位)'
  text='使用者代號請留意英文字母大小寫。若您是使用密碼通知書辦理簽入者，請輸入該密碼通知書序號。'
  placehoder='忘記使用者代號' //在提示框旁邊的文字
/>
```

##### TopTooltip

`TopTooltip` 組件用於在頂部顯示泡泡框。

```jsx
import TopTooltip from './TopTooltip';

<TopTooltip
  title='使用者代號(6-12位)'
  text='使用者代號請留意英文字母大小寫。若您是使用密碼通知書辦理簽入者，請輸入該密碼通知書序號。'
  placehoder='忘記使用者代號' //在提示框旁邊的文字
/>
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

以下是 `Link` 组件的介紹：

### [<ins>連結(Link)</ins>](#%E7%9B%AE%E6%AC%A1)

`Link` 組件是一個通用的連結工具，用於創建不同類型的連結按鈕。這個組件包含多個不同的子組件，每個子組件用於創建特定類型的連結。

#### ICON_TYPE 常數

`ICON_TYPE` 常數包含了多種圖標類型，用於設定 `IconLink` 的圖標樣式。

#### PhoneLink

`PhoneLink` 組件用於創建電話號碼的連結按鈕。

##### 屬性（Props）

| 屬性   | 描述                                               |
| ------ | -------------------------------------------------- |
| phone  | 要連結的電話號碼（必填）                         |
| text   | 顯示的文字，如不設定則使用電話號碼                |

#### HyperLink

`HyperLink` 組件用於創建網址的連結按鈕。

##### 屬性（Props）

| 屬性      | 描述                                                    |
| --------- | ------------------------------------------------------- |
| href      | 要連結的網址                                           |
| text      | 顯示的文字，如不設定則使用網址，如擁有 children 則會優先顯示 |
| children  | 子組件，可替代顯示的文字                               |
| className | 樣式字串                                               |
| target    | 指定連結的打開方式，預設為 `_blank`                  |

#### ImgLink

`ImgLink` 組件用於創建圖片的連結按鈕。

##### 屬性（Props）

| 屬性   | 描述                                           |
| ------ | ---------------------------------------------- |
| href   | 要連結的網址                                  |
| src    | 圖片路徑（必填）                             |
| alt    | 圖片標籤                                     |
| target | 指定連結的打開方式，預設為 `_blank`        |

#### IconLink

`IconLink` 組件用於創建帶有圖標的連結按鈕。

##### 屬性（Props）

| 屬性         | 描述                                                  |
| ------------ | ----------------------------------------------------- |
| href         | 連結的 URL                                           |
| iconType     | 圖標的類型，使用 `ICON_TYPE` 常數（必填）           |
| iconOrderLast| 圖標是否在文本之後顯示，預設為 `false`                |
| onClick      | 點擊事件處理函式                                    |
| target       | 指定連結的打開方式，預設為 `_blank`                 |
| title        | 連結的標題文本                                      |

`Link` 組件可用於創建各種不同類型的連結按鈕，包括電話連結、網址連結、圖片連結以及帶有圖標的連結。這些子組件具有不同的屬性，以滿足各種連結需求。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>表格元件(Table)</ins>](#%E7%9B%AE%E6%AC%A1)

#### 普通表格 (Table.Normal)

普通表格是一個通用的表格組件，支援不同風格的呈現。以下是 `Table.Normal` 的各個變體：

##### Table.Normal.A

`Table.Normal.A` 是普通表格的一個變體，支援以下屬性：

###### 屬性 (Props)

| 屬性                    | 類型               | 描述                                                     |
| ----------------------- | ------------------ | -------------------------------------------------------- |
| `data`                  | `arrayOf(object)`  | 要顯示的資料陣列。                                       |
| `columns`               | `arrayOf(object)`  | 列的配置。                                               |
| `attachClassName`       | `arrayOf(string)`  | 附加到表格的額外 CSS 類名的陣列。                       |
| `wrapWithTableWrapper`  | `bool`             | 是否使用表格包裹器 (TableWrapper)。預設為 `true`。     |

###### 範例

```jsx
import { Table } from 'components/table';

const data = [...]; // 你的資料陣列
const columns = [...]; // 你的列配置

<Table.Normal.A data={data} columns={columns} wrapWithTableWrapper={true} />;
```

##### Table.Normal.B

`Table.Normal.B` 是普通表格的另一個變體，支援以下屬性：

###### 屬性 (Props)

| 屬性                    | 類型               | 描述                                                     |
| ----------------------- | ------------------ | -------------------------------------------------------- |
| `data`                  | `arrayOf(object)`  | 要顯示的資料陣列。                                       |
| `columns`               | `arrayOf(object)`  | 列的配置。                                               |
| `compare`               | `bool`             | 是否顯示比較模式的表頭。預設為 `false`。               |
| `compareLeftTitle`      | `string`           | 比較模式的左側表頭標題。                                 |
| `compareRightTitle`     | `string`           | 比較模式的右側表頭標題。                                 |
| `customThead`           | `node`             | 自定義表格的 `<thead>` 元素。                            |

###### 範例

```jsx
import { Table } from 'components/table';

const data = [...]; // 你的資料陣列
const columns = [...]; // 你的列配置

<Table.Normal.B
  data={data}
  columns={columns}
  compare={true}
  compareLeftTitle="左側標題"
  compareRightTitle="右側標題"
  customThead={<thead>自定義表頭</thead>}
/>;
```

##### Table.Normal.C

`Table.Normal.C` 是普通表格的變體之一，支援以下屬性：

###### 屬性 (Props)

| 屬性                    | 類型               | 描述                                                     |
| ----------------------- | ------------------ | -------------------------------------------------------- |
| `data`                  | `arrayOf(object)`  | 要顯示的資料陣列。                                       |
| `columns`               | `arrayOf(object)`  | 列的配置。                                               |
| `attachClassName`       | `arrayOf(string)`  | 附加到表格的額外 CSS 類名的陣列。                       |

###### 範例

```jsx
import { Table } from 'components/table';

const data = [...]; // 你的資料陣列
const columns = [...]; // 你的列配置

<Table.Normal.C data={data} columns={columns} />;
```

##### Table.Normal.D

`Table.Normal.D` 是普通表格的另一個變體，支援以下屬性：

###### 屬性 (Props)

| 屬性                    | 類型               | 描述                                                     |
| ----------------------- | ------------------ | -------------------------------------------------------- |
| `data`                  | `arrayOf(object)`  | 要顯示的資料陣列。                                       |
| `columns`               | `arrayOf(object)`  | 列的配置。                                               |
| `attachClassName`       | `arrayOf(string)`  | 附加到表格的額外 CSS 類名的陣列。                       |

###### 範例

```jsx
import { Table } from 'components/table';

const data = [...]; // 你的資料陣列
const columns = [...]; // 你的列配置

<Table.Normal.D data={data} columns={columns} />;
```

非常抱歉之前的回答有誤，以下是 `Table.Responsive` 的各個變體的介紹和相關範例，按照您的要求提供：

#### 響應式表格 (Table.Responsive)

響應式表格支援在不同設備上以不同方式呈現表格資料。以下是 `Table.Responsive` 的各個變體：

##### Table.Responsive.Card.A

`Table.Responsive.Card.A` 是響應式表格的一個變體，支援以下屬性：

###### 屬性 (Props)

| 屬性                    | 類型               | 描述                                                     |
| ----------------------- | ------------------ | -------------------------------------------------------- |
| `data`                  | `arrayOf(object)`  | 要顯示的資料陣列。                                       |
| `columns`               | `arrayOf(object)`  | 列的配置。                                               |
| `totalTable`            | `object`           | 包含總計資料的表格配置。                                 |
| `highlightAt`           | `arrayOf(number)`  | 需要高亮顯示的行的索引陣列。                             |

###### 範例

```jsx
import { Table } from 'components/table';

const data = [...]; // 你的資料陣列
const columns = [...]; // 你的列配置
const totalTable = { ... }; // 你的包含總計資料的表格配置
const highlightAt = [0, 2]; // 高亮顯示的行索引

<Table.Responsive.Card.A
  data={data}
  columns={columns}
  totalTable={totalTable}
  highlightAt={highlightAt}
/>;
```

##### Table.Responsive.Card.B

`Table.Responsive.Card.B` 是響應式表格的另一個變體，支援以下屬性：

###### 屬性 (Props)

| 屬性                    | 類型               | 描述                                                     |
| ----------------------- | ------------------ | -------------------------------------------------------- |
| `data`                  | `arrayOf(object)`  | 要顯示的資料陣列。                                       |
| `columns`               | `arrayOf(object)`  | 列的配置。                                               |
| `totalTable`            | `object`           | 包含總計資料的表格配置。                                 |
| `highlightAt`           | `arrayOf(number)`  | 需要高亮顯示的行的索引陣列。                             |

###### 範例

```jsx
import { Table } from 'components/table';

const data = [...]; // 你的資料陣列
const columns = [...]; // 你的列配置
const totalTable = { ... }; // 你的包含總計資料的表格配置
const highlightAt = [0, 2]; // 高亮顯示的行索引

<Table.Responsive.Card.B
  data={data}
  columns={columns}
  totalTable={totalTable}
  highlightAt={highlightAt}
/>;
```

#### Table.Responsive.Card.C

`Table.Responsive.Card.C` 是響應式表格的元件之一，它支援下列屬性：

##### 屬性 (Props)

| 屬性 | 類型 | 描述 |
| ---------- | ---------------- | --------------------- - |
| `data` | `arrayOf(object)` | 要顯示的資料數組。 |
| `columns` | `arrayOf(object)` | 列的設定。 |

##### 範例

```jsx
import { Table } from 'components/table';

const data = [...]; // 你的資料數組
const columns = [...]; // 你的列配置

<Table.Responsive.Card.C
   data={data}
   columns={columns}
/>;
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

##### Table.Responsive.Sticky.A

`Table.Responsive.Sticky.A` 是響應式表格的一個變體，支援以下屬性：

###### 屬性 (Props)

| 屬性                    | 類型               | 描述                                                     |
| ----------------------- | ------------------ | -------------------------------------------------------- |
| `data`                  | `arrayOf(object)`  | 要顯示的資料陣列。                                       |
| `columns`               | `arrayOf(object)`  | 列的配置。                                               |
| `leftFixedColumnLength` | `number`           | 左側固定列的數量。                                       |
| `totalColumns`          | `arrayOf(object)`  | 包含總計資料的列配置。                                   |
| `limitSets`             | `arrayOf(object)`  | 列的限制配置。                                           |

###### 範例

```jsx
import { Table } from 'components/table';

const data = [...]; // 你的資料陣列
const columns = [...]; // 你的列配置
const leftFixedColumnLength = 2; // 左側固定列的數量
const totalColumns = [...]; // 你的包含總計資料的列配置
const limitSets = [...]; // 你的列的限制配置

<Table.Responsive.Sticky.A
  data={data}
  columns={columns}
  leftFixedColumnLength={leftFixedColumnLength}
  totalColumns={totalColumns}
  limitSets={limitSets}
/>;
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>PDF元件(PdfGenerator)</ins>](#%E7%9B%AE%E6%AC%A1)

PdfGenerator 是一個用於生成 PDF 文件的 React 組件。它支援不同的呈現方式和使用情境。

#### 屬性 (Props)

| 屬性                          | 類型         | 描述                                                                                                         |
| ----------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------ |
| `renderElement`               | `function`  | 一個函數，返回您希望轉換為 PDF 的 React 元素。                                                            |
| `renderFunction`              | `function`  | 一個函數，返回您希望轉換為 PDF 的內容。                                                                    |
| `renderRef`                   | `ref`       | 一個 React 引用，指向您希望轉換為 PDF 的元素。                                                           |
| `renderApi`                   | `string`    | 一個 API 路徑，用於獲取要轉換為 PDF 的內容。                                                               |
| `filename`                    | `string`    | 所生成 PDF 文件的文件名。                                                                                   |
| `modal`                       | `bool`      | 是否顯示 PDF 預覽模態窗口。                                                                                |
| `modalTitle`                  | `string`    | PDF 預覽模態窗口的標題。                                                                                    |
| `modalSerial`                 | `string`    | PDF 文件的序列號。                                                                                          |
| `showDownloadBtn`             | `bool`      | 是否在預覽模態窗口中顯示下載按鈕。                                                                        |
| `onBefore`                    | `function`  | 在生成 PDF 之前觸發的函數。                                                                                |
| `onFinal`                     | `function`  | 在 PDF 生成完成後觸發的函數。                                                                              |
| `onDisagree`                  | `function`  | 在使用者不同意的情況下觸發的函數。                                                                        |
| `onAgree`                     | `function`  | 在使用者同意的情況下觸發的函數。                                                                        |
| `onDocumentError`             | `function`  | 如果生成 PDF 時發生錯誤，則觸發的函數。                                                                 |
| `onError`                     | `function`  | 如果在生成 PDF 期間發生錯誤，則觸發的函數。                                                             |
| `shouldCloseOnBackdropClick`  | `bool`      | 點擊背景時是否關閉 PDF 預覽模態窗口。                                                                  |

#### 範例

##### 使用 `downloadPdf` 方法：

```jsx
import PdfGenerator from 'components/PdfGenerator';

<PdfGenerator>{({ downloadPdf }) => <button onClick={downloadPdf}>下載 PDF</button>}</PdfGenerator>;
```

##### 使用 `generatePdfByApi` 方法：

```jsx
import PdfGenerator from 'components/PdfGenerator';

<PdfGenerator renderApi="api path">{({ generatePdfByApi }) => <button onClick={generatePdfByApi}>生成 PDF</button>}</PdfGenerator>;
```

##### 使用 `generatePdfByRef` 方法：

```jsx
import PdfGenerator from 'components/PdfGenerator';

const myRef = React.createRef();

<PdfGenerator renderRef={myRef}>{({ generatePdfByRef }) => <button onClick={generatePdfByRef}>生成 PDF</button>}</PdfGenerator>;
```

##### 使用 `generatePdfByElement` 方法：

```jsx
import PdfGenerator from 'components/PdfGenerator';

<PdfGenerator renderElement={<div>這是一個 React 元素，將轉換為 PDF。</div>}>
  {({ generatePdfByElement }) => <button onClick={generatePdfByElement}>生成 PDF</button>}
</PdfGenerator>;
```

##### 使用 `generatePdfByFunction` 方法：

```jsx
import PdfGenerator from 'components/PdfGenerator';

<PdfGenerator renderFunction={() => '這是一個 PDF 內容的文字描述。'}>
  {({ generatePdfByFunction }) => <button onClick={generatePdfByFunction}>生成 PDF</button>}
</PdfGenerator>;
```

#### Modal 屬性

如果 `modal` 屬性設置為 `true`，將會顯示 PDF 預覽模態窗口，以供用戶預覽和操作 PDF 文件。這將在生成 PDF 後彈出模態窗口，用戶可以預覽 PDF、下載 PDF，或執行其他操作。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>分頁(Pagination)</ins>](#%E7%9B%AE%E6%AC%A1)

Pagination 組件是一個用於顯示分頁控制元素的 React 組件。它可以用於處理大量資料的分頁，允許用戶輕鬆地瀏覽不同頁面的內容。

#### 屬性 (Props)

| 屬性            | 類型     | 描述                                                                                                                                                                                                                                       |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `onPageChange`  | `func`   | 當頁面更改時使用更新後的頁面值調用的回調函數。當用戶單擊分頁控制按鈕時，此函數將被調用，並且新的頁面號碼將作為參數傳遞。                                                                                                        |
| `totalCount`    | `number` | 表示源中可用資料的總數。Pagination 組件使用此總數來計算分頁的數量和頁面號碼。                                                                                                                                                            |
| `siblingCount`  | `number` | （可選）：表示要在當前頁面按鈕的每一側顯示的頁面按鈕的最小數量。默認為 1。這決定了在當前頁面左右兩側顯示多少個分頁按鈕。                                                                                                    |
| `currentPage`   | `number` | 表示當前活動頁面。Pagination 組件將使用基於 1 的索引（而不是傳統的基於 0 的索引）來表示當前頁面值。這意味著頁面號碼從 1 開始而不是從 0 開始。                                                                                     |
| `pageSize`      | `number` | 表示單頁可見的最大資料量。這用於計算分頁，確定每個頁面上顯示多少資料項。                                                                                                                                                                |

#### 範例

以下是如何使用 Pagination 組件的示例：

```jsx
import React, { useState } from 'react';
import Pagination from './Pagination';

function App() {
  const [currentPage, setCurrentPage] = useState(1);
  const pageSize = 10; // 每頁顯示的資料量

  // 當頁面更改時的回調函數
  const handlePageChange = (newPage) => {
    setCurrentPage(newPage);
    // 在這裡你可以根據新的頁面號碼從後端獲取對應頁面的資料
  };

  // 模擬總資料量
  const totalCount = 100;

  return (
    <div>
      {/* 顯示 Pagination 組件 */}
      <Pagination
        onPageChange={handlePageChange}
        totalCount={totalCount}
        currentPage={currentPage}
        pageSize={pageSize}
      />

      {/* 在這裡根據當前頁面和 pageSize 從資料源中顯示相應資料 */}
      <div>
        {`顯示第 ${(currentPage - 1) * pageSize + 1} 到 ${(currentPage - 1) * pageSize + pageSize} 條資料`}
      </div>
    </div>
  );
}

export default App;
```

上面的示例演示了如何在應用程序中使用 Pagination 組件來處理分頁。當用戶單擊分頁按鈕時，`onPageChange` 回調函數被觸發，您可以在其中編寫代碼以根據新的頁面號碼從後端獲取相應的資料。 Pagination 組件會根據總資料量、當前頁面和 `pageSize` 屬性來自動生成分頁按鈕。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>入口(Portal)</ins>](#%E7%9B%AE%E6%AC%A1)

`Portal` 組件是一個實用的工具，它封裝了 React 中的 `createPortal` 函數，允許你輕鬆將子組件渲染到應用程式的 `document.body` 元素上。這對於創建模態對話框、通知或需要在應用程式的不同 DOM 結構位置顯示的元素非常有用。

#### 如何使用

使用 `Portal` 組件非常簡單。只需將你希望渲染的子組件作為 `children` 傳遞給 `Portal` 組件即可。`Portal` 組件將使用 `createPortal` 函數將這些子組件渲染到應用程式的 `document.body` 元素上。

#### 範例

以下是一個使用 `Portal` 組件的示例：

```javascript
import React from 'react';
import Portal from './Portal';

function App() {
    return (
        <div>
            <h1>我的應用程式</h1>
            <Portal>
                <div className="模態對話框">
                    <h2>模態對話框</h2>
                    <p>這個模態對話框是使用 portal 渲染的，並顯示在應用程式的其他元素之上。</p>
                </div>
            </Portal>
        </div>
    );
}

export default App;
```

在這個示例中，`Portal` 組件將 `<div className="模態對話框">` 元素渲染到應用程式的 `document.body` 元素上，使它能夠獨立顯示在應用程式的其他元素之上。

#### 工作原理

`Portal` 組件在渲染時使用 `createPortal` 函數創建一個獨立的 DOM 容器，然後將其附加到 `document.body` 上。接著，它將子組件渲染到這個獨立容器中，使它們能夠顯示在應用程式的 `document.body` 元素上，而不是其他 DOM 元素之中。這對於需要在應用程式的不同 DOM 結構位置顯示元素的情況非常有用。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>畫面遮罩(Loading)</ins>](#%E7%9B%AE%E6%AC%A1)

`Loading` 組件是一個用於顯示頁面載入狀態的 React 組件。通常，當應用程序需要載入資源或執行長時間操作時，可以使用此組件來提供視覺指示，告訴用戶正在處理中。

#### 使用方式

```javascript
import React from 'react';
import Loading from './Loading';

// 在您的應用程序中，根據需要使用 Loading 組件
const MyComponent = () => {
  const isLoading = true; // 設置為 true 以顯示載入指示符
  return (
    <div>
      <p>Some content here...</p>
      <Loading isLoading={isLoading} />
      <p>More content here...</p>
    </div>
  );
};

export default MyComponent;
```

#### 屬性

- `isLoading`（必需）：一個布林值，用於控制是否顯示載入指示符。當 `isLoading` 為 `true` 時，`Loading` 組件將顯示載入指示符；當 `isLoading` 為 `false` 時，它將隱藏。

#### 載入指示符和畫面遮罩

- `Loading` 組件提供了一個畫面遮罩，當 `isLoading` 為 `true` 時，它會顯示一個載入指示符，同時防止用戶在載入期間導航到其他頁面元素。

- 載入指示符：載入指示符是一個簡單的動畫元素，用於告知用戶應用程序正在處理中。當 `isLoading` 為 `true` 時，載入指示符將顯示在整個畫面上。

- 畫面遮罩：畫面遮罩是一個半透明的背景層，將整個畫面覆蓋，以防止用戶與頁面其他部分互動。這可以防止用戶在載入期間進行任何操作，提高用戶體驗。

#### 示例

在上面的示例中，將 `Loading` 組件嵌入到 `MyComponent` 中，並根據需要將 `isLoading` 設置為 `true` 或 `false` 以控制載入指示符的顯示。當應用程序處於載入狀態時，`Loading` 組件顯示一個載入指示符和畫面遮罩，告訴用戶操作正在進行中，同時防止他們進行其他操作。這有助於提高用戶體驗並確保用戶不會在載入過程中遇到問題。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>列表(ListItem)</ins>](#%E7%9B%AE%E6%AC%A1)

`ListItem` 組件是一個多功能的列表組件，可用於呈現不同類型的列表，包括數字列表、圓點列表、中文數字列表、註解數字符號列表等。它提供了各種列表樣式的選擇，並可以自訂外觀。

#### 列表組件常數

在 `ListItem` 組件中，你可以使用以下常數以指定列表的寬度：

- `LISTITEM_WIDTH.WIDTH_FULL`：寬度全屏
- `LISTITEM_WIDTH.WIDTH_990`：寬度 990px
- `LISTITEM_WIDTH.WIDTH_750`：寬度 750px
- `LISTITEM_WIDTH.WIDTH_800`：寬度 800px
- `LISTITEM_WIDTH.WIDTH_375`：寬度 375px

以及以下列表的類型：

- `LISTITEM_TYPE.OL`：數字列表
- `LISTITEM_TYPE.UL`：圓點列表
- `LISTITEM_TYPE.DL`：定義列表

#### 列表組件的通用 propType

`ListItem` 組件具有通用的 propType，它可以應用於不同類型的列表。以下是通用的 propType：

- `type`：列表的類型，可以是 'ol'（數字列表）、'ul'（圓點列表）或 'dl'（定義列表）。
- `items`：包含列表項目的數組，每個項目可以是字符串或 React 元素。
- `width`：用於指定列表容器的寬度。
- `attachClassName`：要附加到列表容器的樣式類名的數組。
- `classnames`：用於指定每個列表項目的類名的數組。

#### 列表組件的類型

`ListItem` 組件包含多種不同類型的列表：

- `NumberedListItem`：數字列表組件，可以自訂樣式和寬度。
- `BulletListItem`：圓點列表組件，同樣可以自訂樣式和寬度。
- `ChineseNumberedListItem`：中文數字列表組件，支援自訂樣式和寬度。
- `NoteNumberedListItem`：註解數字符號列表組件，可自訂樣式和寬度。
- `ParenthesizedNumberedListItem`：括弧數字列表組件，支援自訂樣式和寬度。
- `HalfStarListItem`：半形星號列表組件，同樣可以自訂樣式和寬度。
- `FullStarListItem`：全形星號列表組件，支援自訂樣式和寬度。
- `TipsListItem`：提醒文字列表清單組件，可自訂樣式和寬度。
- `ChineseParenthesizedNumberedListItem`：中文括弧數字列表組件，同樣支援自訂樣式和寬度。

使用這些不同的列表組件，可以靈活地創建和自訂不同樣式和類型的列表，以滿足需求。

<div style='page-break-before: always; height: 0; width: 0;'></div>

## [<ins>共用工具</ins>](#%E7%9B%AE%E6%AC%A1)

共用工具位於 src/common/utils 目錄下，打開會看到以下的結構。

- arithmeticHelper.js
- blobHelpers.js
- browserHelpers.js
- chipCardHelper.js
- formatArray.js
- formatCheck.js
- formatDate.js
- formatNumber.js
- getApiResponse.js
- getComponentDisplayName.js
- type.js

### [<ins>arithmeticHelper</ins>](#%E7%9B%AE%E6%AC%A1)

`arithmeticHelper` 是一個位於 `src/common/utils` 目錄下的工具檔案，提供了一些有關數學運算的輔助功能。

#### `getRandomNumber(min, max)`

這個函數用於生成指定範圍內的隨機整數。

- `min`（必須）：指定範圍的最小值（包括）。
- `max`（必須）：指定範圍的最大值（包括）。

它將返回一個介於 `min` 和 `max` 之間（包括這兩個數字）的隨機整數。

#### `generateArithmeticQuestion(operator)`

這個函數用於生成帶有指定運算符號的四則運算題目和答案。

- `operator`（可選）：運算符號，可選值包括 `+`, `-`, `*`, `/`。如果未提供，它將隨機選擇一個運算符號。

根據運算符號，它將生成不同類型的運算題目和答案，如下：

- `+` 或 `-` 運算符號：生成一個包含兩個數字的加法或減法題目，其中第一個數字是 2 位數，介於 10 到 99 之間，第二個數字是 1 位數，介於 1 到 9 之間。
- `*` 運算符號：生成一個包含兩個數字的乘法題目，其中兩個數字都是 1 位數，介於 1 到 9 之間。
- `/` 運算符號：生成一個包含兩個數字的除法題目，其中第一個數字是能夠整除第二個數字的數字，介於 1 到 81 之間，第二個數字是 1 位數，介於 1 到 9 之間，確保除法結果是整數。

它將返回一個包含運算題目和答案的物件，其中包括以下屬性：

- `question`：運算題目的字串表示，例如 `"23 + 5"`。
- `answer`：運算答案，是一個數字，例如 `28`。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>blobHelpers</ins>](#%E7%9B%AE%E6%AC%A1)

`blobHelpers` 是一個位於 `src/common/utils` 目錄下的工具檔案，提供了一個有關 Blob 物件操作的輔助功能。

#### `downloadBlob(blob, filename = '')`

這個函數用於下載包含在 Blob 物件中的檔案到使用者的本地端。你可以傳遞一個 Blob 物件，以及選擇性的檔案名稱。

- `blob`（必須）：包含要下載內容的 Blob 物件。
- `filename`（可選）：下載的檔案名稱，預設為空字串。如果未提供檔案名稱，則會使用時間戳記作為檔案名稱。

這個函數的操作過程如下：

1. 創建 Blob 物件的 URL，以便瀏覽器可以訪問 Blob 內容。
2. 創建一個隱藏的 `<a>` 元素。
3. 如果提供了檔案名稱，將該檔案名稱設定為 `<a>` 元素的 `download` 屬性；否則，使用時間戳記作為檔案名稱。
4. 將 Blob 的 URL 設定為 `<a>` 元素的 `href` 屬性。
5. 在網頁的 `<body>` 元素中添加該 `<a>` 元素。
6. 模擬點擊 `<a>` 元素，觸發下載操作。
7. 從 `<body>` 元素中移除該 `<a>` 元素。

這樣，Blob 中的檔案將以指定的檔案名稱下載到使用者的本地端。

### [<ins>browserHelpers</ins>](#%E7%9B%AE%E6%AC%A1)

`browserHelpers` 包含了一系列有關瀏覽器和操作系統的輔助功能。以下是這些功能的簡介：

#### `getOperatingSystem()`

這個函數用於獲取使用者的作業系統。它會檢查使用者代理字串以識別作業系統，並返回作業系統的名稱。支援的作業系統包括 Windows、macOS、Linux、Android、iOS 等。

#### `getScreenResolution()`

此函數用於獲取螢幕的解析度，並返回以寬x高的格式表示的字串，例如："1920x1080"。

#### `getBrowserVersion()`

這個函數用於獲取瀏覽器的名稱和版本資訊。它會檢查使用者代理字串以識別瀏覽器，並返回包含瀏覽器名稱和版本資訊的字串。

#### `getJavaScriptVersion()`

這個函數用於獲取 JavaScript 的版本資訊。它會分析使用者代理字串以確定 JavaScript 的版本，然後返回版本號。

#### `isBrowser64Bit()`

此函數用於檢查瀏覽器是否為 64 位元的。它會檢查使用者代理字串以確定瀏覽器是否是 64 位元的，並返回布林值（true 或 false）。

#### `getContextPath()`

這個函數用於獲取網站的 "context path"，通常是網站的根目錄名稱。它會解析目前網頁的 URL 以找到 context path。

#### `getTxnUrl(systemCode, categoryCode, functionCode, route = '/01')`

此函數用於組合出對應的交易路徑。根據傳入的系統代碼、分類代碼、功能代碼和路徑後綴，它會生成交易路徑的 URL。這在需要在不同交易之間跳轉時非常有用。

#### `getStaticUrl(path)`

這個函數用於生成完整的靜態資源 URL。它接受一個路徑 (path) 參數並根據目前網頁的 URL 生成完整的靜態資源 URL。

### [<ins>chipCardHelper</ins>](#%E7%9B%AE%E6%AC%A1)

`chipCardHelper` 包含了一系列有關晶片金融卡的輔助功能。以下是這些功能的簡介：

#### `getChipCardErrorKeyByCode(code)`

此函數用於根據晶片金融卡的錯誤狀態碼（`code` 參數）取得對應的 i18n 鍵值（國際化鍵值）。這些鍵值通常用於顯示錯誤訊息或警告訊息，以便向使用者解釋發生的錯誤。函數內部使用 `switch` 語句，根據不同的錯誤狀態碼返回對應的鍵值。如果提供的錯誤狀態碼不在 `switch` 語句的案例中，則函數會返回一個預設的鍵值，通常是指未預期的錯誤。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>formatArray</ins>](#%E7%9B%AE%E6%AC%A1)

`formatArray` 包含了一個有關陣列處理的輔助函數，這個函數用於將傳入的字串陣列轉換為物件。該物件的鍵（keys）將是原始字串陣列中的字串值，而值（values）將是傳入的參數 `val`。這個函數的主要用途是將一組字串陣列轉換為一個方便用於樣式或類名管理的物件，通常可以與 `classnames` 套件等一起使用。

#### `fStrsToOneObj(arr, val)`

此函數接受兩個參數：`arr` 和 `val`。`arr` 是傳入的字串陣列，`val` 則是傳入的參數。函數使用 `reduce` 方法來遍歷 `arr` 中的每個字串，然後將它們映射到一個物件中，其中鍵是字串的值，值是傳入的 `val`。最後，函數返回這個物件，其中包含了轉換後的對應關係。

以下是一個使用範例：

```javascript
const classNames = ['form-check', 'form-check-inline'];
const classNamesObj = fStrsToOneObj(classNames, true);
```

在這個範例中，`classNamesObj` 將成為以下物件：

```javascript
{
    'form-check': true,
    'form-check-inline': true
}
```

這個物件可用於動態組合樣式或類名，以根據需要設定或取消特定的樣式類別。

### [<ins>formatCheck</ins>](#%E7%9B%AE%E6%AC%A1)

`formatCheck` 包含了一系列的輔助函數，用於檢查不同類型的資料格式或執行特定的檢查操作。這些函數可用於確保資料的合法性，執行格式驗證，以及檢查瀏覽器功能的支持情況。

#### 字符串格式驗證函數

1. `isIdNumber(val)`
   - 用於驗證身份證號碼格式是否合法。
   - 接受一個字符串 `val` 作為參數，並返回布爾值，表示是否合法。

2. `isEmail(email)`
   - 用於驗證電子郵件地址的格式是否合法。
   - 接受一個字符串 `email` 作為參數，並返回布爾值，表示是否合法。

3. `isValidAlphanumericFormat(str, length)`
   - 用於驗證字串是否符合指定長度的英數字格式。
   - 接受兩個參數，`str` 為要驗證的字串，`length` 為要求的字串長度。
   - 返回布爾值，表示是否符合要求。

4. `isValidNumericFormat(str, length)`
   - 用於驗證字串是否符合指定長度的數字格式。
   - 接受兩個參數，`str` 為要驗證的字串，`length` 為要求的字串長度。
   - 返回布爾值，表示是否符合要求。

5. `isStrLengthInRange(str, min, max, strictMode = false)`
   - 用於檢查字串的長度是否在指定範圍內。
   - 接受四個參數，`str` 為要檢查的字串，`min` 和 `max` 為最小和最大長度，`strictMode` 為是否啟用嚴格模式。
   - 返回布爾值，表示字串長度是否在指定範圍內。

6. `isValidDecimalLength(str, decimalCount = 0)`
   - 用於判斷輸入的字串是否為合法的十進位數字格式，且小數點後的位數不超過指定長度。
   - 接受兩個參數，`str` 為要判斷的字串，`decimalCount` 為小數點後的位數不超過的長度。
   - 返回布爾值，表示是否符合要求。

#### 資料類型檢查函數

7. `isInt(val)`
   - 用於檢查值是否為整數。
   - 接受一個參數 `val`，並返回布爾值，表示是否為整數。

8. `isEmpty(val)`
   - 用於檢查值是否為空（未定義、null 或長度為0的字串或陣列）。
   - 接受一個參數 `val`，並返回布爾值，表示是否為空。

9. `isOneOfEmpty(...vals)`
   - 用於檢查多個值中是否至少有一個是空的。
   - 接受多個參數 `...vals`，並返回布爾值，表示是否至少有一個是空的。

10. `isObject(val)`
    - 用於檢查值是否為物件。
    - 接受一個參數 `val`，並返回布爾值，表示是否為物件。

11. `isFunction(val)`
    - 用於檢查值是否為函數。
    - 接受一個參數 `val`，並返回布爾值，表示是否為函數。

12. `isString(val)`
    - 用於檢查值是否為字串。
    - 接受一個參數 `val`，並返回布爾值，表示是否為字串。

13. `isBoolean(val)`
    - 用於檢查值是否為布爾值。
    - 接受一個參數 `val`，並返回布爾值，表示是否為布爾值。

14. `isNumber(val)`
    - 用於檢查值是否為數字。
    - 接受一個參數 `val`，並返回布爾值，表示是否為數字。

15. `isArray(val)`
    - 用於檢查值是否為陣列。
    - 接受一個參數 `val`，並返回布爾值，表示是否為陣列。

16. `isUndef(val)`
    - 用於檢查值是否為未定義。
    - 接受一個參數 `val`，並返回布爾值，表示是否為未定義。

#### 瀏覽器功能支持檢查函數

17. `isMobile()`
    - 用於檢查設備是否為移動設備。
    - 返回布爾值，表示是否為移動設備。

18. `isTablet()`
    - 用於檢查設備是否為平板設備。
    - 返回布爾值，表示是否為平板設備。

19. `isWithinDaysBefore(dateString, days)`
    - 用於判斷日期字串是否在今天以前的指定天數範圍內。
    - 接受兩個參數，`dateString` 為日期字串（yyyyMMdd 格式），`days` 為指定的天數。
    - 返回布爾值，表示日期是否在指定天數範圍內。

20. `isWithinDaysAfter(dateString, days)`
    - 用於判斷日期字串是否在今天以後的指定天數範圍內。
    - 接受兩個參數，`dateString` 為日期字串（yyyyMMdd 格式），`days` 為指定的天數。
    - 返回布爾值，表示日期是否在指定天數範圍內。

21. `isWithinYearsBefore(dateString, years)`
    - 用於判斷日期字串是否在今天以前的指定年數範圍內。
    - 接受兩個參數，`dateString` 為日期字串（yyyyMMdd 格式），`years` 為指定的年數。
    - 返回布爾值，表示日期是否在指定年數範圍內。

22. `isWithinYearsAfter(dateString, years)`
    - 用於判斷日期字串是否在今天以後的指定年數範圍內。
    - 接受兩個參數，`dateString` 為日期字串（yyyyMMdd 格式），`years` 為指定的年數。
    - 返回布爾值，表示日期是否在指定年數範圍內。

23. `isWithinMonthsBefore(dateString, months)`
    - 用於判斷日期字串是否在今天以前的指定月數範圍內。
    - 接受兩個參數，`dateString` 為日期字串（yyyyMMdd 格式），`months` 為指定的月數。
    - 返回布爾值，表示日期是否在指定月數範圍內。

24. `isWithinMonthsAfter(dateString, months)`
    - 用於判斷日期字串是否在今天以後的指定月數範圍內。
    - 接受兩個參數，`dateString` 為日期字串（yyyyMMdd 格式），`months` 為指定的月數。
    - 返回布爾值，表示日期是否在指定月數範圍內。

25. `isBeforeToday(dateString)`
    - 用於判斷日期字串是否在今天以前。
    - 接受一個參數 `dateString`，為日期字串（yyyyMMdd 格式）。
    - 返回布爾值，表示日期是否在今天以前。

#### 瀏覽器功能支持檢查函數

26. `isGetUserMediaSupported()`
    - 用於檢查瀏覽器是否支持 `getUserMedia` 方法（用於訪問媒體設備，如攝像頭和麥克風）。
    - 返回布爾值，表示瀏覽器是否支持 `getUserMedia` 方法。

這些函數提供了各種常見的資料驗證和檢查功能，可用於不同的應用場景，以確保資料的合法性和應用的正確性。

### [<ins>formatDate</ins>](#%E7%9B%AE%E6%AC%A1)

`formatDate` 包含了一系列的日期格式化函數，用於將日期或時間轉換成特定格式的字符串。

#### `toIntOrStr(str)`
   - 這個函數用於將輸入的字符串轉換為整數，如果輸入的字符串是數字。
   - 如果輸入的字符串無法轉換為整數，則返回當前時間的時間戳（整數表示）。
   - 接受一個參數 `str`，為要轉換的字符串。
   - 返回轉換後的整數值或時間戳。

#### `getTwLocaleString(time)`
   - 這個函數用於將日期/時間轉換為台灣繁體中文的本地化日期時間字符串格式。
   - 接受一個參數 `time`，為要進行格式化的日期/時間。該參數可以是整數或字符串。
   - 返回台灣繁體中文格式的本地化日期時間字符串，包括年、月、日、時、分、秒，並且不使用12小時制。

#### `getYMDHMS(time, symbol = '/')`
   - 這個函數用於將日期/時間轉換為指定的年月日時分秒格式的字符串。
   - 接受兩個參數，`time` 為要進行格式化的日期/時間，可以是整數或字符串；`symbol` 為分隔日期和時間部分的符號，預設為 `/`。
   - 返回指定格式的日期時間字符串，包括年、月、日、時、分、秒，各部分使用指定的分隔符號分隔。

#### `getYMD(time, symbol = '/')`
   - 這個函數用於將日期/時間轉換為指定的年月日格式的字符串。
   - 接受兩個參數，`time` 為要進行格式化的日期/時間，可以是整數或字符串；`symbol` 為分隔年、月、日部分的符號，預設為 `/`。
   - 返回指定格式的年月日字符串，各部分使用指定的分隔符號分隔。

#### `getTwYMD(time, symbol = '')`
   - 這個函數用於將日期/時間轉換為台灣繁體中文的年月日格式的字符串。
   - 接受兩個參數，`time` 為要進行格式化的日期/時間，可以是整數或字符串；`symbol` 為用於替換日期部分的分隔符號，預設為空字串。
   - 返回台灣繁體中文格式的年月日字符串，各部分使用指定的分隔符號分隔。

這些函數提供了方便的日期格式轉換功能，可根據需求將日期或時間轉換為不同的格式，用於顯示或處理日期資料。

### [<ins>formatNumber</ins>](#%E7%9B%AE%E6%AC%A1)

`formatNumber` 包含了一系列的數字格式化函數，用於處理數字和字串中的數字部分。

#### `addThousandSeparator(str, separator = ',')`
   - 這個函數用於將傳入的數字或包含小數的字串加上千分位符號，使數字更易讀。
   - 接受兩個參數，`str` 為要進行格式化的字串，`separator` 為千分位符號，預設為逗號 `,`。
   - 如果輸入的字串不是有效的數字或包含小數，則返回原始字串。否則，將數字部分的千分位加入，並保留小數部分。

#### `removeSymbol(str)`
   - 這個函數用於將傳入的字串中的數字以外的符號去除，只保留數字部分。
   - 接受一個參數 `str`，為要進行處理的字串。
   - 返回去除非數字字符後的新字串，只包含數字。

這些函數提供了方便的數字處理功能，可用於格式化數字的顯示或處理，以及將字串中的數字提取出來進行計算或比較。

### [<ins>getApiResponse</ins>](#%E7%9B%AE%E6%AC%A1)

`getApiResponse` 包含了一個函數，用於解析 API 回應的格式，並返回一個包含多個元素的 Tuple 狀態結構。這個函數可用於簡化 API 回應的處理。

#### `getApiResponse(response)`
   - 這個函數用於解析 API 回應，並返回一個包含多個元素的 Tuple。
   - 接受一個參數 `response`，為 API 回應物件。
   - 返回一個包含以下元素的 Tuple：
     1. 是否交易成功 (`true` 或 `false`)，根據回應中的 `ResponseCode` 判斷是否成功。
     2. 回傳訊息 (`ResponseMessage`)，包含有關回應的文字訊息。
     3. 回傳資料 (`ResponseData`)，包含回應的資料。
     4. 回傳日期時間 (`ResponseDT`)，回應的日期和時間。
     5. 回傳代碼 (`ResponseCode`)，表示回應的狀態碼。

此函數使得在處理 API 回應時更加方便，可以輕鬆地從回應中提取必要的信息，並判斷交易是否成功。

### [<ins>getComponentDisplayName</ins>](#%E7%9B%AE%E6%AC%A1)

`getComponentDisplayName` 包含了一個函數，用於獲取 React 組件的顯示名稱（displayName）。顯示名稱通常用於調試消息，以便識別特定的 React 組件。通常情況下，顯示名稱是從定義組件的函數或類的名稱自動推斷出來的。但在某些情況下，你可能需要明確設置顯示名稱，例如在創建高階組件時。

#### `getComponentDisplayName(WrappedComponent)`
   - 這個函數接受一個參數 `WrappedComponent`，它是一個 React 組件。
   - 函數的作用是獲取組件的顯示名稱（displayName）。
   - 如果組件具有 `displayName` 屬性，則返回該屬性的值。
   - 否則，如果組件具有 `name` 屬性，則返回該屬性的值。
   - 如果都沒有，則返回默認值 `'Component'`。

這個函數可以在開發 React 應用時用於更好地識別和調試組件。如果需要明確指定一個自定義的顯示名稱，你可以使用這個函數來實現。

### [<ins>type</ins>](#%E7%9B%AE%E6%AC%A1)

`type` 包含了一系列用於定義常數的 JavaScript 對象。這些常數通常用於應用程序中的各種配置、設置和定義中，以確保代碼的一致性和可讀性。以下是 `type.js` 中定義的一些主要常數對象：

1. `RESPONSE_CODE`：定義了 API 響應的不同狀態代碼，例如成功（SUCCESS）、錯誤（E002、E004 等）等。

2. `CUSTOM_EVENT`：定義了自定義事件的名稱，這些事件可以在應用程序中使用，如交易暫停（TXN_SUSPENDED）、資料時間（TXN_DATA_TIME）等。

3. `CURRENCY_CODE`：定義了不同貨幣的代碼，如台幣（TWD）、美元（USD）等。

4. `MSG_CODE`：定義了不同消息的代碼，如成功消息（R0001）、錯誤消息（P0001）等。

5. `BUTTON_STATE`：定義了按鈕的不同狀態，如主要（PRIMARY）、漸變（GRADIENT）、灰色（GRAY）等。

6. `ICON_TYPE`：定義了不同圖標的類型，如 PDF、Word、Excel 等。

7. `BUTTON_TYPE`：定義了按鈕的類型，如提交（SUBMIT）和普通（BUTTON）。

8. `BUTTON_SIZE`：定義了按鈕的大小，如大（LARGE）、正常（NORMAL）、小（SMALL）。

9. `INPUT_TYPE`：定義了輸入元素的不同類型，如文本（TEXT）、密碼（PWD）、郵件（EMAIL）等。

10. `MIME_TYPE`：定義了不同 MIME 類型的常數，用於檔案上傳等操作。

11. `TOOLTIP_TYPE`：定義了工具提示的不同類型，如頂部（TOP）、右側（RIGHT）、底部（BOTTOM）等。

12. `COLOR_CODE`：定義了一組顏色代碼。

13. `SUPPORT_OS`：定義了支持的操作系統，如 Windows 和 macOS。

14. `ANNOUNCEMENT_TITLE_STYLE`：定義了公告標題的不同風格，如純文本（PLAIN_TEXT）、HTML 內容（HTML_CONTENT）和鏈接（LINK）。

這些常數對象可以在應用程序中引入並使用，以確保代碼的可讀性和維護性。通常，它們用於配置和設置不同部分的行為，或者用於處理不同的應用程序邏輯場景。

<div style='page-break-before: always; height: 0; width: 0;'></div>

## [<ins>自定義 Hooks 介紹</ins>](#%E7%9B%AE%E6%AC%A1)

自定義 Hooks 共用工具位於 src/common/hooks目錄下，打開會看到以下的結構。
- useBreadcrumbs.js
- useCountdown.js
- useDebounce.js
- useE2EE.js
- useForm.js
- useFrame.js
- useLoadTime.js
- useLocalStorage.js
- usePageLoading.js
- usePagination.js
- useSCSBWebATM.js
- useSettings.js
- useThrottle.js
- useToggle.js
- useTxnLog.js

### [<ins>useBreadcrumbs</ins>](#%E7%9B%AE%E6%AC%A1)

`useBreadcrumbs` 是一個實用的 React Hook，它為您的應用程式提供了一個簡單而有效的方法，來協助設定和管理交易畫面的麵包屑（Breadcrumbs）。麵包屑是一種在網站或應用程式界面中常見的導航元素，它們可以讓使用者追蹤他們的位置並返回先前的頁面。

#### 用法

首先，需要引入 `useBreadcrumbs`：

```javascript
import useBreadcrumbs from '/common/hooks/useBreadcrumbs';
```

然後，在 React 組件中使用 `useBreadcrumbs` Hook。需要提供以下參數：

- `breadcrumbs`（必需）：頁面麵包屑的多語系設定資料陣列，例如：
  
  ```javascript
  breadcrumbs: [
      { i18nKey: ['FX.05.BREADCRUMBS.BREADCRUMBS_1', { ns: 'twde' }] },
      { i18nKey: ['FX.05.BREADCRUMBS.BREADCRUMBS_2', { ns: 'twde' }] },
      { i18nKey: ['FX.05.BREADCRUMBS.BREADCRUMBS_3', { ns: 'twde' }] },
  ]
  ```

- `i18nKey`（可選）：頁面標題對應的多語系鍵值。

- `namespace`（可選）：多語系命名空間。

<div style='page-break-before: always; height: 0; width: 0;'></div>

例如，可以在組件中使用 `useBreadcrumbs` 如下：

```javascript
useBreadcrumbs(breadcrumbs, i18nKey, namespace);
```

#### 功能

`useBreadcrumbs` Hook 的主要功能是為了協助設定和管理交易畫面的麵包屑。它根據您提供的多語系設定資料陣列，自動翻譯麵包屑的文本，並將其設定為應用程式的麵包屑。這使得麵包屑的管理變得簡單而高效，無需手動處理翻譯和更新。

### [<ins>useCountdown</ins>](#%E7%9B%AE%E6%AC%A1)

`useCountdown` 是一個自定義的 React Hook，它允許您在應用程式中實現倒數計時功能。這對於需要倒數計時的場景，例如驗證碼倒數、計時遊戲或其他時間敏感應用非常有用。

#### 用法

首先，需要引入 `useCountdown`：

```javascript
import { useCountdown } from '/common/hooks/useCountdown';
```

然後，可以在 React 組件中使用 `useCountdown` Hook。以下是一個示例：

```javascript
const [countdown, { reset, toggle, isPause }] = useCountdown({
    initial: true,       // 是否初始化時就開始倒數
    seconds: 5,          // 倒數的秒數
    intervalMs: 1000,    // 倒數的間隔，單位為毫秒
    callback: () => {
        console.log('Countdown finished!');
    }
});
```

#### 功能

`useCountdown` Hook 提供了以下功能：

- `countdown`：當前的倒數秒數。您可以將它嵌入到您的 UI 中以顯示倒數時間。

- `reset` 函數：用於重置倒數計時。當呼叫 `reset` 函數時，倒數計時將被重置為初始設定的秒數。

- `toggle` 函數：用於暫停或啟動倒數計時。當呼叫 `toggle` 函數時，倒數計時將在暫停和啟動之間切換。

- `isPause`：表示當前倒數計時是否處於暫停狀態。

可以根據需求配置初始值、倒數秒數、間隔時間以及倒數完成後的回調函數。這使得在應用程式中實現各種倒數計時場景變得輕鬆。

### [<ins>useDebounce</ins>](#%E7%9B%AE%E6%AC%A1)

`useDebounce` 是一個自定義的 React Hook，用於實現防抖功能。防抖是一種常用於處理頻繁觸發事件的技術，它可以確保在指定的時間間隔內只執行一次回調函數，從而減少不必要的計算和請求。

#### 用法

首先，需要引入 `useDebounce`：

```javascript
import { useDebounce } from '/common/hooks/useDebounce';
```

然後，可以在 React 組件中使用 `useDebounce` Hook。以下是一個示例：

```javascript
const greet = () => { 
    console.log('Hello'); 
};

const debounced = useDebounce(greet, 1500);

// 在某個事件處理函數中使用防抖函數
const handleInputChange = (event) => {
    // 在指定的時間間隔內只執行一次 greet 函數
    debounced();
};
```

#### 功能

`useDebounce` Hook 提供了以下功能：

- 防抖效果：當使用 `useDebounce` 創建一個防抖函數後，該函數將確保在指定的時間間隔內只執行一次回調函數。如果在指定時間間隔內多次觸發該函數，它將以最後一次觸發的時間為基準重新計時。

- 設定時間間隔：可以指定防抖的時間間隔（以毫秒為單位）。這決定了在多長時間內多次觸發的事件將被合併為單一的執行。

- 動態更新回調函數：可以隨時更改回調函數，並且新的回調函數將在防抖函數執行時生效。

`useDebounce` 非常適用於處理用戶輸入的實時搜索建議、處理窗口大小變化事件、節流 HTTP 請求等場景，以減少不必要的計算和資源浪費。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useE2EE</ins>](#%E7%9B%AE%E6%AC%A1)

`useE2EE` 是一個自定義的 React Hook，用於實現端對端加密（End-to-End Encryption，簡稱 E2EE）的功能。端對端加密是一種安全通訊的方式，它確保資料在發送方和接收方之間加密，只有接收方能夠解密和讀取資料，而其他人無法進行中間的監視或干擾。

#### 用法

首先，需要引入 `useE2EE`：

```javascript
import { useE2EE } from '/common/hooks/useE2EE';
```

然後，可以在 React 組件中使用 `useE2EE` Hook。以下是一個示例：

```javascript
const { encryptData } = useE2EE();

const userId = 'user123';
const idNumber = '1234567890';
const pwd = 'password123';

// 將需要加密的資料傳遞給 encryptData 函數
const [[encryptedData1, encryptedData2, encryptedData3], encryptionKey] = await encryptData(userId, idNumber, pwd);
```

#### 功能

`useE2EE` Hook 提供了以下功能：

- 端對端加密（E2EE）：它使用 RSA 和 AES 加密算法，將資料在發送和接收之間進行加密和解密，確保資料的機密性。

- 加密金鑰生成：它能夠生成用於資料加密和解密的加密金鑰，並且定期更新。

- 加密資料：可以將需要加密的資料傳遞給 `encryptData` 函數，它將返回加密後的資料和加密金鑰。

- 錯誤處理：如果加密過程中出現錯誤，它將返回 `null`，並且在控制台中記錄錯誤信息。

`useE2EE` 非常適用於需要保護敏感資料的應用程序，例如用戶身份驗證信息、個人資訊等。它確保資料在傳輸過程中是安全的，只有合法的接收方能夠解密和使用這些資料。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useForm</ins>](#%E7%9B%AE%E6%AC%A1)

`useForm` 是一個自定義的 React Hook，用於簡化表單管理和處理的過程。它允許您輕鬆地追蹤表單的狀態，處理表單資料的變化，以及設置表單的初始資料。

#### 用法

首先，需要引入 `useForm`：

```javascript
import useForm from '/common/hooks/useForm';
```

然後，可以在 React 組件中使用 `useForm` Hook。以下是一個示例：

```javascript
const initialFormState = {
    username: { value: '', errorMsg: '' },
    email: { value: '', errorMsg: '' },
    password: { value: '', errorMsg: '' }
};

const [formState, inputHandler, setFormData] = useForm(initialFormState);
```

#### 功能

`useForm` Hook 提供了以下功能：

- 表單狀態管理：它通過 `formState` 對象來追蹤表單的當前狀態，包括每個表單字段的值和錯誤信息。

- 表單資料處理：可以使用 `inputHandler` 函數來處理表單字段的變化。它接受三個參數：`id`（表單字段的唯一標識符）、`value`（新的字段值）和 `errorMsg`（錯誤消息）。當字段值發生變化時，它會更新 `formState` 並返回 `true`，如果有錯誤消息則返回 `false`。

- 設置初始資料：可以使用 `setFormData` 函數來設置表單的初始資料。它接受一個包含表單字段的對象，並將其應用於 `formState`。

`useForm` 可以幫助您更有效地管理表單資料和錯誤處理，並提供一致的方法來處理表單輸入。這使得開發和維護表單頁面變得更加容易。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useMenuDuplicateTxnRender</ins>](#%E7%9B%AE%E6%AC%A1)

`useMenuDuplicateTxnRender` 是一個自定義的 React Hook，用於處理選單重複進入相同交易的情況。這個 Hook 通過監聽特定自訂事件來實現功能，當檢測到重複進入相同交易時，將執行提供的回調函數。

#### 用法

首先，需要引入 `useMenuDuplicateTxnRender`：

```javascript
import useMenuDuplicateTxnRender from '/common/hooks/useMenuDuplicateTxnRender';
```

然後，可以在 React 組件中使用 `useMenuDuplicateTxnRender` Hook。以下是一個示例：

```javascript
const handleDuplicateTxnRender = () => {
    // 執行處理交易重複透過選單進入的邏輯
    console.log('處理交易重複透過選單進入');
};

// 在組件中使用 useMenuDuplicateTxnRender Hook
useMenuDuplicateTxnRender(handleDuplicateTxnRender);
```

#### 功能

`useMenuDuplicateTxnRender` Hook 提供了以下功能：

- 自定義事件監聽：它在窗口上添加了一個自訂事件監聽器，用於監聽選單重複渲染交易事件。

- 回調函數執行：當檢測到重複進入相同交易時，它將執行提供的回調函數。

- 內存清理：它還返回一個函數，用於清除事件監聽器，以避免內存洩漏。

`useMenuDuplicateTxnRender` 適用於需要處理特定自訂事件的情況，例如在選單重複渲染交易時執行特定邏輯。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useFrameResources</ins>](#%E7%9B%AE%E6%AC%A1)

`useFrameResources` 是一個 React Hook，用於在進入點處理引入框架通用資源，這些資源包括 favicon、CSS 樣式表和 JavaScript 檔案。通常，這個 Hook 用於應用程式的進入點，以確保在應用程式初始化時載入所需的資源。

#### 用法

首先，要引入 `useFrameResources`：

```javascript
import { useFrameResources } from '/common/hooks/useFrameResources';
```

然後，在應用程式的進入點處使用 `useFrameResources` Hook：

```javascript
function App() {
    useFrameResources();

    // ... 其他應用程式邏輯
}
```

#### 功能

`useFrameResources` Hook 提供了以下功能：

- 載入 favicon：它會在 `<head>` 標籤中動態創建一個 `<link>` 元素，並設置其 `rel` 和 `href` 屬性以引入網站的 favicon。

- 載入 CSS 樣式表：它會在 `<head>` 標籤中動態創建多個 `<link>` 元素，並設置其 `rel` 和 `href` 屬性以引入 CSS 樣式表。這些樣式表通常用於定義網站的外觀和風格。

- 載入 JavaScript 檔案：它會在 `<body>` 標籤的末尾動態創建多個 `<script>` 元素，並設置其 `src` 屬性以引入 JavaScript 檔案。這些檔案通常包含框架或庫，以增強應用程式的功能。

- 清理資源：當組件卸載時，`useFrameResources` 會自動清理所引入的資源，以避免內存洩漏或資源殘留。

使用這個 Hook 可以確保應用程式在初始化時具有所需的資源，並在組件卸載時清理這些資源，從而提高應用程式的效能和可維護性。這尤其適用於需要引入多個外部資源的大型應用程式。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useFrameDisableContextMenu</ins>](#%E7%9B%AE%E6%AC%A1)

`useFrameDisableContextMenu` 是一個 React Hook，用於在進入點禁用右鍵菜單（context menu）。

#### 用法

首先，要引入 `useFrameDisableContextMenu`：

```javascript
import { useFrameDisableContextMenu } from '/common/hooks/useFrameDisableContextMenu';
```

然後，在應用程式的進入點處使用 `useFrameDisableContextMenu` Hook：

```javascript
function App() {
    useFrameDisableContextMenu();

    // ... 其他應用程式邏輯
}
```

#### 功能

`useFrameDisableContextMenu` Hook 提供了以下功能：

- 禁用右鍵菜單：當組件渲染時，它會綁定一個事件監聽器，以在特定區域內禁用右鍵菜單。這意味著當用戶右鍵單擊組件內的元素時，不會觸發右鍵菜單。

- 清理事件監聽器：當組件卸載時，`useFrameDisableContextMenu` 會自動刪除所添加的事件監聽器，以確保不會出現內存洩漏或殘留的事件監聽器。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useLoadTime</ins>](#%E7%9B%AE%E6%AC%A1)

`useLoadTime` 是一個自定義的 React Hook，用於計算組件載入的時間。它可以幫助您監控組件載入所需的時間，以便進行性能分析和優化。

#### 用法

首先，需要引入 `useLoadTime`：

```javascript
import useLoadTime from '/common/hooks/useLoadTime';
```

然後，在要監控載入時間的組件中使用 `useLoadTime` Hook：

```javascript
function MyComponent() {
    const loadTime = useLoadTime();

    // ... 組件的其他邏輯

    return (
        <div>
            {/* 顯示載入時間 */}
            <p>組件載入時間：{loadTime} 毫秒</p>
            {/* ... */}
        </div>
    );
}
```

#### 功能

`useLoadTime` Hook 提供了以下功能：

- 監控組件載入時間：它使用 `performance.now()` 函數來獲取載入開始時間和載入結束時間，並計算它們之間的時間差，從而獲得組件的載入時間。

- 返回載入時間：它將計算得到的載入時間（以毫秒為單位，取整數）作為狀態返回，以便可以在組件中使用它。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useLocalStorage</ins>](#%E7%9B%AE%E6%AC%A1)

`useLocalStorage` 是一個用來在 React 應用程序中使用 LocalStorage 的自定義 Hook。它提供了方便的方法來存儲、讀取、更新和刪除本地存儲中的資料。

#### 用法

首先，需要引入 `useLocalStorage`：

```javascript
import useLocalStorage from '/common/hooks/useLocalStorage';
```

然後，在組件中使用 `useLocalStorage` Hook：

```javascript
function MyComponent() {
    // 定義 LocalStorage 的鍵和預設值
    const key = 'myDataKey';
    const defaultValue = { value: 'default' };

    // 使用 useLocalStorage Hook，獲取資料和設定資料的函數
    const [data, setData] = useLocalStorage(key, defaultValue);

    // ... 組件的其他邏輯

    return (
        <div>
            {/* 顯示從 LocalStorage 中獲取的資料 */}
            <p>Data from LocalStorage: {data.value}</p>
            {/* ... */}
        </div>
    );
}
```

#### 功能

`useLocalStorage` Hook 提供了以下功能：

- 讀取 LocalStorage 中的資料：當組件初始化時，它會嘗試讀取指定鍵的資料。如果找不到資料，它將使用預設值。

- 更新 LocalStorage 中的資料：組件可以使用 `setData` 函數來更新 LocalStorage 中的資料。該函數接受一個新的值或一個回調函數，並將其保存到 LocalStorage 中。

- 移除 LocalStorage 中的資料：組件可以使用 `removeValueFromLocalStorage` 函數來刪除 LocalStorage 中指定鍵的資料。

- 檢查 LocalStorage 中是否存在資料：組件可以使用 `isExistValueFromLocalStorage` 函數來檢查指定鍵的資料是否存在於 LocalStorage 中。

- 檢查 LocalStorage 中是否存在任何資料：組件可以使用 `isExistAnyValueFromLocalStorage` 函數來檢查是否存在任何資料於 LocalStorage 中。

- 清空 LocalStorage 中的所有資料：組件可以使用 `clearLocalStorage` 函數來清空 LocalStorage 中的所有資料。

#### 鍵的命名規定

請注意，為了確保 LocalStorage 中的資料能夠正確辨識和管理，應遵守以下鍵的命名規定：

- 鍵的前八碼必須使用相關交易的唯一代號。
- 這個規則確保了資料在 LocalStorage 中的唯一性，避免不同交易或操作之間的衝突，以及機制處理。

遵守這個規則可以確保的應用程序在使用 `useLocalStorage` 時，能夠正確地辨識和管理各種資料，從而提高了程式碼的可讀性和可維護性。

#### 注意事項

- 使用 `key` 參數：請根據命名規定，使用具有意義的鍵，以確保資料能夠正確識別。

- 使用 `defaultValue` 參數：如果 LocalStorage 中找不到指定的鍵，將使用 `defaultValue` 作為初始值。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>usePageLoading</ins>](#%E7%9B%AE%E6%AC%A1)

`usePageLoading` 是一個用來管理網頁載入狀態的自定義 Hook。它允許您輕鬆地實現畫面遮罩效果，以提示用戶應用程序正在進行某些操作或載入資料。

#### 用法

首先，需要引入 `usePageLoading`：

```javascript
import usePageLoading from '/common/hooks/usePageLoading';
```

然後，在組件中使用 `usePageLoading` Hook：

```javascript
function MyComponent() {
    // 初始化網頁載入狀態為 false（不顯示遮罩）
    const { isPageLoading, runPageLoading, stopPageLoading } = usePageLoading(false);

    // 在需要顯示遮罩的操作中，使用 runPageLoading 啟用遮罩
    const handleDataFetching = async () => {
        runPageLoading();
        // 執行需要時間的操作，例如資料載入
        await fetchData();
        // 操作完成後，使用 stopPageLoading 停用遮罩
        stopPageLoading();
    };

    return (
        <div>
            {/* 根據 isPageLoading 的值來顯示或隱藏遮罩 */}
            {isPageLoading && <div className="loader-overlay">Loading...</div>}
            {/* ... 其他組件內容 */}
        </div>
    );
}
```

#### 功能

`usePageLoading` Hook 提供了以下功能：

- `isPageLoading`：當前網頁載入狀態的布林值，用於控制遮罩的顯示或隱藏。

- `runPageLoading`：用於啟用網頁遮罩，通常在需要顯示載入效果的操作中調用。

- `stopPageLoading`：用於停用網頁遮罩，當操作完成時調用，隱藏遮罩。

#### 注意事項

- 可以在需要的操作中使用 `runPageLoading` 啟用遮罩，然後在操作完成後使用 `stopPageLoading` 停用遮罩，以提供良好的用戶體驗。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>usePagination</ins>](#%E7%9B%AE%E6%AC%A1)

`usePagination` 是一個用於在 React 應用程式中管理分頁功能的自訂 Hook。它允許您輕鬆地生成和管理分頁控制元素，以處理大量資料的分頁顯示。

#### 用法

首先，需要引入 `usePagination`：

```javascript
import usePagination from '/common/hooks/usePagination';
```

然後，在的 React 組件中使用 `usePagination` Hook：

```javascript
function MyComponent() {
    // 定義分頁所需的相關參數
    const totalCount = 100; // 總資料數
    const pageSize = 10; // 每頁顯示的資料量
    const siblingCount = 1; // 左右兄弟頁面按鈕的數量
    const currentPage = 1; // 當前頁面

    // 使用 usePagination Hook，獲取分頁數組
    const paginationRange = usePagination({
        totalCount,
        pageSize,
        siblingCount,
        currentPage
    });

    return (
        <div>
            {/* 顯示分頁控制元素 */}
            <ul className="pagination">
                {paginationRange.map((pageNumber, index) => (
                    <li key={index}>
                        {pageNumber === '...' ? (
                            <span className="dots">{pageNumber}</span>
                        ) : (
                            <button className="page-button">{pageNumber}</button>
                        )}
                    </li>
                ))}
            </ul>
            {/* ... 其他組件內容 */}
        </div>
    );
}
```

#### 功能

`usePagination` Hook 提供了以下功能：

- `totalCount`：表示源中可用資料的總數。

- `pageSize`：表示每頁可見的最大資料量。

- `siblingCount`（可選）：表示要在當前頁面按鈕的每一側顯示的頁面按鈕的最小數量。默認為 1。

- `currentPage`：表示當前活動頁面。

- `paginationRange`：返回一個包含分頁數字和 DOTS（省略號）的數組，您可以在 UI 中使用它來顯示分頁控制元素。

#### 注意事項

- `usePagination` Hook 通過計算分頁數組，幫助您管理分頁控制元素的生成和顯示，以應對大量資料的分頁需求。

### useSettings.js

`useSettings.js` 是一個自定義 hook，旨在簡化在 React 應用程序中訪問設置的過程。這個 hook 可以幫助開發人員更容易地在組件中訪問應用程序的設置，並提供了一個統一的方法。

#### 功能

- 使用 `useContext` 和 `SettingsContext` 引入相關依賴，其中 `SettingsContext` 是一個自定義上下文，用於管理應用程序的設置。

- 提供一個 `useSettings` 函數，用於獲取應用程序的設置上下文。

- 如果 `useSettings` 函數未在 `SettingsProvider` 內使用，則會拋出錯誤，以確保只有在正確的上下文中使用。

- 返回包含設置和相關函數的上下文對象，使組件能夠輕鬆地訪問這些設置。

#### 用法示例

以下是如何在 React 組件中使用 `useSettings` hook 的示例：

```jsx
import React from 'react';
import { useSettings } from './useSettings';

function MyComponent() {
  // 使用 useSettings hook 來獲取設置上下文
  const { settings, updateSettings } = useSettings();

  // 在這裡使用設置和相關函數
  // ...
}

export default MyComponent;
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useThrottle</ins>](#%E7%9B%AE%E6%AC%A1)

`useThrottle` 是一個自定義 hook，用於實現節流（Throttle）功能。節流是一種限制函數執行頻率的技術，它確保在指定時間間隔內只執行一次函數，避免過於頻繁的執行。

#### 功能

- 提供一個 `useThrottle` 函數，可將任意回調函數包裝成節流函數。

- 接受兩個參數：
  - `fn`（必需）：要包裝成節流函數的回調函數。
  - `delay`（必需）：指定時間間隔（以毫秒為單位），在這個時間間隔內的多次觸發將不會執行函數。

- 返回一個包裝後的節流函數，用於替代原始回調函數。

#### 用法示例

以下是如何在 React 組件中使用 `useThrottle` hook 的示例：

```jsx
import React, { useCallback } from 'react';
import { useThrottle } from './useThrottle';

function MyComponent() {
  // 創建一個回調函數
  const greet = useCallback(() => { console.log('Hello'); }, []);

  // 使用 useThrottle hook 將回調函數包裝成節流函數
  const throttled = useThrottle(greet, 1500);

  // 在需要的地方使用節流函數，以確保不會過於頻繁地執行
  const handleClick = () => {
    throttled();
  };

  return (
    <button onClick={handleClick}>Say Hello</button>
  );
}

export default MyComponent;
```

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useToggle</ins>](#%E7%9B%AE%E6%AC%A1)

`useToggle` 是一個自定義 hook，用於管理布林狀態的切換（Toggle）。這個 hook 可以幫助你輕鬆地創建和控制布林值的切換行為。

#### 功能

- 提供一個 `useToggle` 函數，可用於創建布林狀態以及切換該狀態的函數。

- 接受一個初始布林狀態作為參數，並返回一個包含以下兩個屬性的對象：
  - `isToggled`（布林值）：代表當前的狀態。
  - `toggle`（函數）：用於切換狀態的函數。

#### 用法示例

以下是如何在 React 組件中使用 `useToggle` hook 的示例：

```jsx
import React from 'react';
import { useToggle } from './useToggle';

function MyComponent() {
  // 使用 useToggle hook 創建一個布林狀態和切換函數
  const { isToggled, toggle } = useToggle(false);

  return (
    <div>
      <p>狀態：{isToggled ? '已啟用' : '已禁用'}</p>
      <button onClick={toggle}>切換狀態</button>
    </div>
  );
}

export default MyComponent;
```

在這個示例中，`useToggle` 被用來創建一個布林狀態 `isToggled` 和一個切換函數 `toggle`。當用戶點擊 "切換狀態" 按鈕時，狀態將切換為相反的值。

這個 hook 對於管理各種簡單的布林狀態切換非常實用，例如開關、折疊面板等等。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useTxnLog</ins>](#%E7%9B%AE%E6%AC%A1)

`useTxnLog` 是一個自定義 hook，旨在協助處理應用程序中的交易日誌記錄。它提供了一個方式來發送日誌資料到後端，同時還提供了相關的工具和資料類型以便簡化日誌記錄的管理。

#### `LogDTO` 日誌資料傳輸物件

`LogDTO` 是一個用於結構化日誌信息的類。它包含了以下屬性：

- `Page`：頁面識別號
- `PageName`：頁面名稱
- `Step`：步驟識別號
- `StepName`：步驟名稱
- `TimeSpend`：花費的時間
- `Payload`：其他自定義資料

使用 `LogDTO` 類可以幫助組織和驗證日誌信息。它提供了相應的 setter 和 getter 方法，以及一個 `toDataObj` 方法，用於將日誌信息轉換為資料對象。

#### `recordLog` 紀錄日誌函數

`recordLog` 函數是一個柯里化（Currying）方法，用於記錄日誌。它接受一個 `LogDTO` 對象作為參數，然後返回一個回調函數。這個回調函數可以接受成功和失敗的回調函數，並在記錄日誌後調用相應的回調函數。

#### `fetchData`、`handleFetchError` 和 `fetchWrapper` 函數

這些函數用於處理從前端到後端的資料發送過程。`fetchData` 用於發送 POST 請求，`handleFetchError` 用於處理錯誤，而 `fetchWrapper` 用於封裝和處理這些過程。

#### `useTxnLog` Hook

最終，`useTxnLog` 是這個自定義 hook 的主要函數，它包括以下功能：

- 使用 `useLoadTime` hook 獲取頁面載入時間。
- 使用 `useLocation` hook 獲取當前路由信息，提取交易 ID。
- 創建一個柯里化的 `recordLog` 函數，並將其包裝在 `useMemo` 中以優化性能。
- 返回一個包含 `recordLog`、`pageLoadTime` 和 `LogDTO` 屬性的對象，使它們可以在組件中使用。

這個 hook 可以方便地用於記錄交易日誌，並提供了結構化和優化的方法來處理日誌記錄的需求。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>useSCSBWebATM</ins>](#%E7%9B%AE%E6%AC%A1)

該`Hook`是整合WebATM安控軟體，提供了多個功能來執行與智慧卡相關的操作。
> 其安控軟體API手冊「SCSB_API手冊_用戶端WebATM安控軟體(WebATM元件).docx」   
> 位於 scsb-bank-frontend/doc/SCSBWebATM 目錄下。  

使用方法就如一般的自訂 `React Hook`，總計 10 種功能

| No | Name | Type | Purpose |
| :----: | :----: | :----: | :----: |
| 1 | isSCSBWebATMInitialized | boolean | 表示 SCSBWebATM 是否資源已經初始化的標記。 |
| 2 | initSCSBWebATMAdapter | function | 初始化 SCSBWebATMAdapter 的函數。 |
| 3 | getCode | function | 獲取錯誤代碼的函數。 |
| 4 | connectCard | function | 連結卡片的函數。 |
| 5 | disconnectCard | function | 中斷與卡片的連結。 |
| 6 | getReaderList | function | 獲取讀卡機列表的函數。 |
| 7 | getVersion | function | 取得底層元件版本號的函數。 |
| 8 | getCardStatus | function | 取得卡片狀態的函數。 |
| 9 | getSCSBAccount | function | 得到持卡人基本資料的函數。 |
| 10 | verifyPIN | function | 傳送 PIN 碼至晶片金融卡進行密碼驗證的函數。 |

交易開發比較常用功能應該為:  
`No.1`、`No.3`、`No.6`、`No.8`、`No.9`、`No.10`  
其餘為組件內部自控或擴充性提供之功能。  

在`Hook`提供的功能函式中，有分為同步/異步函數 :  
- 同步（Synchronous）:  
`No.2`、`No.3`、`No.5`、`No.6`、`No.7`  
- 異步（Asynchronous）:  
`No.4`、`No.8`、`No.9`、`No.10`  

而除了`No.2`、`No.3`以外，  
所有的功能函式都會回傳一個統一結構的物件，  
物件包含了`code`和`data`屬性，
> `code`代表錯誤代碼，如果為 `0` 表示成功，其他代碼請查照API手冊。  
> `data`代表回傳的資料。
> 
> 回傳的資料則視函數結果可能會是`undefined`、`string`、`array`等型態，  
> 各個函數註解中皆會標記清楚，再請查閱。

<br/>

#### 同步和異步函數如何使用 ?

舉例來說`No.6`為同步函數，就如以下代碼一般使用即可  

```javascript
const fetchReaderList = () => {
    const { code, data } = getReaderList();
    console.debug('fetchReaderList code', code);
    console.debug('fetchReaderList data', data);
};
```

而異步函數的話，可以採取兩種方式去實現(以`No.9`為例)  
1. 使用 `async/await`：  
    `async/await` 是一種讓處理異步操作更加簡潔和直觀的語法。
    在定義異步函數時，我們在函數前加上 `async` 關鍵字，然後使用 `await` 關鍵字來等待異步操作的完成。
    這樣，當程式碼執行到 `await` 這一行時，會暫停並等待 `Promise` 的解析，然後將 `Promise` 的結果返回。  
    
    例如:  
    ```javascript
    async function fetchSCSBAccount(readerName) {
        console.debug('fetchSCSBAccount readerName', readerName);
        const { code, data } = await getSCSBAccount(readerName);
        console.debug('fetchSCSBAccount code', code);
        console.debug('fetchSCSBAccount data', data);
    }
    ```
2. 使用 `then`：  
    另一種處理異步操作的方式是使用 `then` 方法，它是 `Promise` 的一個方法，用於處理 `Promise` 的解析和拒絕狀態。
    通過 `then` 方法，我們可以在 `Promise` 解析時處理返回的資料，也可以在拒絕時處理錯誤。  
    
    例如:  
    ```javascript
    function fetchSCSBAccount(readerName) {
        getSCSBAccount(readerName).then(({ code, data }) => {
        	console.debug('fetchSCSBAccount readerName', readerName);
        	console.debug('fetchSCSBAccount code', code);
        	console.debug('fetchSCSBAccount data', data);
        });
    }
    ```
    
#### 各功能介紹

> 代碼也有提供 `JSDoc` 註解:  

- getCode - 獲取錯誤代碼的函數。
  > 取得元件API回傳碼
  > 常見代碼如下，其他代碼請查照API手冊。   
  > `0`:     執行成功。   
  > `5908`:  不被允許使用本元件。    
  > `61001`: ServiSign 一般性錯誤(未正常啟動ServiSign主程式)。    
  > `5070`:  使用者取消操作。  
  > `5071`:	密碼不正確。  
  > `3020`:  表示密碼規則長度有問題。  
  > `61203`: ServiSign 版本錯誤。
  > `61006`: 無法與ServiSign建立連線。

- isSCSBWebATMInitialized - 表示 SCSBWebATM 是否資源已經初始化的標記。
  > 組件初次渲染時初始化 SCSBWebATM 元件。  
  > 如果需要在 SCSBWebATM 元件資源初始化完成判斷狀態代碼時，  
  > 可以搭配 `useEffect` Hook 和 `getCode` 函式
  > ```javascript
  > useEffect(() => {
  >   if (isSCSBWebATMInitialized) {
  >     console.log('useEffect getCode', getCode());
  >   }
  > }, [getCode, isSCSBWebATMInitialized]);
  > ```

- initSCSBWebATMAdapter - 初始化 SCSBWebATMAdapter 的函數。
  > 用來初始化 SCSB WebATM，基本上`Hook`內部會自控，也提供該功能使用。 

- connectCard - 連結卡片的函數。
  > 連結卡片，基本上`Hook`內部會自控，也提供該功能使用。 

- disconnectCard - 中斷與卡片的連結。
  > 中斷與卡片的連結，基本上`Hook`內部會自控，也提供該功能使用。

- getReaderList - 獲取讀卡機列表的函數。
  > 獲取讀卡機列表  
  > 回傳的資料是字串陣列，裡面會是讀卡機名稱  
  > 可以將其資料經過處理作為下拉式選單來源，  
  > 交易控制選擇之讀卡機名稱，再以此操控其餘功能。  

- getVersion - 取得底層元件版本號的函數。
  > 取得底層元件版本號，提供該功能使用。

- getCardStatus - 傳入讀卡機名稱，取得卡片狀態的函數。
  > 輸出代碼，其他代碼請查照API手冊  
  > 0:     已插入。  
  > 3011: 未接上任何讀卡機。  
  > 3005: 卡片不存在、卡片異常或無法判別的卡片。  
  > 3999: 一般性錯誤未插入。  
  > 
  > 經測試，假如故意帶入不存在之讀卡機名稱，則會返回 3005

- getSCSBAccount - 傳入讀卡機名稱，得到持卡人基本資料的函數。
  > 得到持卡人基本資料。
  > 
  > 卡片檔案資料數組內容順序:  
  > - 發卡單位代號(長度8)
  > - 晶片卡備註欄(長度30)
  > - 帳號1(長度16)
  > - 帳號2(長度16)
  > - 帳號3(長度16)
  > - 帳號4(長度16)
  > - 帳號5(長度16)
  > - 帳號6(長度16)
  > - 帳號7(長度16)
  > - 帳號8(長度16)

- verifyPIN - 傳送 讀卡機名稱 和 PIN 碼至晶片金融卡進行密碼驗證的函數。
  > 若`PIN`帶空值 + 一代讀卡機，則由元件跳出畫面輸入。  
  > 若`PIN`帶空值 + 二代讀卡機，則由讀卡機鍵盤輸入。  
  > 若`PIN`有帶入值 + 一代讀卡機，元件將值直接帶入卡片進行驗證。  
  > 若`PIN`有帶入值 + 二代讀卡機，則元件將值帶入卡片後，使用者需再於讀卡機上按下確認鍵。  

- getTsacAndTsn - 傳送 讀卡機名稱 和 TAC參數組合、PIN 碼取得TAC值、交易序號。
  > 得到TAC值、交易序號。
  > 
  > 數組內容順序:  
  > - TAC值
  > - 晶片卡備註欄(長度30)
  > - 交易序號

<div style='page-break-before: always; height: 0; width: 0;'></div>

## [<ins>共用 HOC</ins>](#%E7%9B%AE%E6%AC%A1)

共用 Higher Order Component (HOC) 位於 src/common/hocs 目錄下，打開會看到以下的結構。

- withKeyboard.js
- withLazyLoading.jsx
- withLoadable.jsx
- withOverwriteProps.jsx
- withTxnPageLoaded.js
- withWrappedByDiv.jsx

### [<ins>withKeyboard 高階元件</ins>](#%E7%9B%AE%E6%AC%A1)

`withKeyboard` 是一個高階組件 (HOC)，它用於在 React 組件中集成虛擬鍵盤功能。這個 HOC 可以使你的 React 組件支援虛擬鍵盤，以便在需要的時候啟用鍵盤輸入。

使用 `withKeyboard` 高階組件的步驟如下：

1. 引入 `withKeyboard`：
   
   ```javascript
   import withKeyboard from './withKeyboard';
   ```

2. 將你的組件包裹在 `withKeyboard` 中：

   ```javascript
   const MyComponentWithKeyboard = withKeyboard(MyComponent);
   ```

   其中 `MyComponent` 是你想要添加虛擬鍵盤功能的 React 組件。

3. 使用包裹後的新組件 `MyComponentWithKeyboard`，它現在已經支援虛擬鍵盤功能。

這樣，你的組件就能夠在需要時啟用虛擬鍵盤，並可以通過 `Keyboard` 組件來實現鍵盤輸入功能。

請確保在集成了 `withKeyboard` 的組件中正確使用 `Keyboard` 組件，以實現所需的鍵盤功能。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>withLazyLoading 高階元件</ins>](#%E7%9B%AE%E6%AC%A1)

`withLazyLoading` 是一個高階元件（HOC），它用於為 React 組件添加懶加載（Lazy Loading）的功能。懶加載是一種優化技術，它使應用程序能夠僅在需要時才動態載入組件，從而減少初始載入時間和資源使用。

#### 使用方式

```javascript
import withLazyLoading from './withLazyLoading';

// 將要進行懶加載的組件傳遞給 withLazyLoading
const MyLazyComponent = withLazyLoading(MyComponent);
```

#### 參數

- `LazyComponent`（必需）：要進行懶加載的目標組件，它是一個 React 組件類型。

- `fallback`（可選）：懶加載過程中顯示的指示元素。預設為 `null`，表示不顯示任何指示元素。

#### 如何工作

`withLazyLoading` 包裹的組件在初始載入時不會立即載入。相反，它將使用 React 的 `Suspense` 和 `lazy` 功能進行懶加載。當包裹的組件需要呈現時，`fallback` 指示元素將顯示在組件載入期間。

一旦 `LazyComponent` 完全載入並可用，它將取代 `fallback`，並且應用程序將呈現實際的目標組件。

#### 範例

```javascript
import React from 'react';
import withLazyLoading from './withLazyLoading';

// 創建一個簡單的 React 組件
const MyComponent = () => (
  <div>
    <h1>Hello, Lazy World!</h1>
  </div>
);

// 使用 withLazyLoading 包裹組件，預設 fallback 為 null
const MyLazyComponent = withLazyLoading(MyComponent);

// 在應用程序中呈現 MyLazyComponent
const App = () => (
  <div>
    <p>Some content here...</p>
    <MyLazyComponent />
    <p>More content here...</p>
  </div>
);

export default App;
```

在上面的示例中，`MyComponent` 被包裹在 `withLazyLoading` 中，因此它將以懶加載方式載入。在 `MyLazyComponent` 還未載入完全之前，可以使用 `fallback` 參數指定的指示元素顯示載入進度或其他內容。

藉由使用 `withLazyLoading`，可以優化應用程序的初始載入性能，僅在需要時才載入組件，提供更好的用戶體驗。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>withLoadable 高階元件</ins>](#%E7%9B%AE%E6%AC%A1)

`withLoadable` 高階元件是一個用於提供全版面遮罩式載入特效的 React 高階元件。它通常用於實現組件的懶加載（Lazy Loading），當需要載入資源或執行複雜操作時，它可以在載入期間顯示全版面的遮罩，提供視覺指示。

#### 使用方式

```javascript
import React from 'react';
import withLoadable from './withLoadable';

// 要進行特效載入的組件
const MyComponent = () => {
  return (
    <div>
      {/* 內容 */}
    </div>
  );
};

// 使用 withLoadable 包裝組件以提供全版面遮罩式載入特效
const LoadableMyComponent = withLoadable(MyComponent);

export default LoadableMyComponent;
```

#### 屬性

- `Component`（必需）：要進行特效載入的組件。這是一個 React 組件，通常是希望實現懶加載的組件。

#### 全版面遮罩式載入特效

- `withLoadable` 高階元件通過包裝提供了全版面遮罩式載入特效。當使用 `LoadableMyComponent` 組件時，如果 `MyComponent` 需要載入資源或處理耗時操作，將顯示全版面的遮罩，以告知操作正在進行中。

- 載入特效遮罩：載入特效遮罩是一個用 `<Suspense>` 元件包裝的 `<Loading>` 組件，當 `MyComponent` 載入時，它將顯示全版面的遮罩，提供載入特效。遮罩中通常包含一個載入指示符，提供視覺反饋。

#### 示例

在上面的示例中，有一個名為 `MyComponent` 的組件，希望對其實現懶加載。通過使用 `withLoadable` 高階元件，`MyComponent` 被包裝在 `LoadableMyComponent` 中，這使得當 `MyComponent` 被載入時，將顯示一個全版面的遮罩，提供載入特效。這有助於優化用戶體驗，讓用戶知道操作正在進行中。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>withOverwriteProps 高階元件</ins>](#%E7%9B%AE%E6%AC%A1)

`withOverwriteProps` 高階元件是一個用於動態附加屬性至 React 組件的工具。它允許您將新的屬性（`attach`）附加到包裹的組件上，以擴展或修改該組件的行為或呈現。

#### 使用方式

```javascript
import React from 'react';
import withOverwriteProps from './withOverwriteProps';

// 要包裝的組件
const MyComponent = ({ message }) => {
  return (
    <div>
      <p>{message}</p>
    </div>
  );
};

// 使用 withOverwriteProps 包裝組件以附加新屬性
const EnhancedComponent = withOverwriteProps(MyComponent)({ message: 'Hello, World!' });

export default EnhancedComponent;
```

#### 函數簽名

- `withOverwriteProps(WrappedComponent: React.ComponentType) => (attach: object) => React.ComponentType`

#### 參數

- `WrappedComponent`（必需）：要包裝的 React 組件。這是您希望對其附加新屬性的組件。

- `attach`（必需）：一個包含要附加到 `WrappedComponent` 的新屬性的物件。

#### 附加新屬性

- `withOverwriteProps` 高階元件接受 `WrappedComponent` 作為參數，並返回一個新的組件 `RenderWrapComponent`。當 `RenderWrapComponent` 被渲染時，它將使用 `attach` 中的屬性來擴展 `props`。

- 在示例中，`EnhancedComponent` 是通過將 `{ message: 'Hello, World!' }` 附加到 `MyComponent` 上創建的。因此，當 `EnhancedComponent` 被呈現時，它將具有一個名為 `message` 的新屬性，其值為 `'Hello, World!'`。

#### 示例

在上面的示例中，`MyComponent` 是一個簡單的 React 組件，它接受一個 `message` 屬性並顯示它。通過使用 `withOverwriteProps` 高階元件，將 `{ message: 'Hello, World!' }` 附加到 `MyComponent` 上，並創建了 `EnhancedComponent`。當 `EnhancedComponent` 被呈現時，它將具有 `message` 屬性，這將覆蓋 `MyComponent` 原本的屬性，並顯示 `'Hello, World!'`。這使得可以動態地修改組件的屬性，以達到不同的呈現或行為效果。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>withTxnPageLoaded 高階元件</ins>](#%E7%9B%AE%E6%AC%A1)

`withTxnPageLoaded` 高階元件是一個用於加載交易頁面前進行必要的準備工作的工具。通常用於交易頁面，它可以處理與服務器的通信、錯誤處理以及交易頁面的延遲加載。

#### 使用方式

```javascript
import React from 'react';
import withTxnPageLoaded from './withTxnPageLoaded';

// 設定交易路徑和交易頁面組件
const txnPath = '/example-transaction';
const TransactionPage = React.lazy(() => import('./TransactionPage'));

// 使用 withTxnPageLoaded 包裝交易頁面組件
const EnhancedTransactionPage = withTxnPageLoaded(txnPath, TransactionPage);

export default EnhancedTransactionPage;
```

#### 函數簽名

- `withTxnPageLoaded(txnPath: string, pageComponent: React.Component) => React.Component`

#### 參數

- `txnPath`（必需）：交易路徑，用於向服務器發送請求，確保交易的有效性。

- `pageComponent`（必需）：交易頁面組件，通常是使用 `React.lazy` 延遲加載的。

#### 功能和流程

- `withTxnPageLoaded` 高階元件接受交易路徑 `txnPath` 和交易頁面組件 `pageComponent` 作為參數。它將返回一個新的 React 組件 `WithTxnPageLoaded`。

- `WithTxnPageLoaded` 組件將處理以下操作：

    1. 發送與服務器的通信：在組件渲染後，它將向服務器發送請求，以驗證交易的有效性。如果交易路徑 `txnPath` 存在，則將發送請求。

    2. 處理服務器響應：當服務器回應時，它將處理服務器的響應。如果響應成功，則會設置相關的資料。如果響應失敗，則會處理錯誤並設置錯誤狀態。

    3. 延遲加載交易頁面：它使用 `withLoadable` 高階元件對 `pageComponent` 進行延遲加載，以確保只在需要時才加載交易頁面。

    4. 處理錯誤：如果發生錯誤，則 `WithTxnPageLoaded` 組件將使用錯誤邊界處理錯誤，以確保交易頁面不會因錯誤而崩潰。

#### 示例

在上面的示例中，我們設定了交易路徑 `txnPath` 和交易頁面組件 `TransactionPage`，然後使用 `withTxnPageLoaded` 高階元件將它們包裝在一起。這使得我們可以確保在載入交易頁面之前進行必要的準備工作，包括與服務器的通信和錯誤處理。這對於確保交易頁面的可靠性和效能至關重要。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>withTxnPageLoaded 高階元件</ins>](#%E7%9B%AE%E6%AC%A1)

`withTxnPageLoaded` 高階元件用於加載交易頁面前的必要準備工作，通常用於交易頁面，它能處理與服務器的通信、交易暫停以及交易頁面的延遲加載。

#### 使用方式

```javascript
import React from 'react';
import withTxnPageLoaded from './withTxnPageLoaded';

// 設定交易路徑和交易頁面組件
const txnPath = '/example-transaction';
const TransactionPage = React.lazy(() => import('./TransactionPage'));

// 使用 withTxnPageLoaded 包裝交易頁面組件
const EnhancedTransactionPage = withTxnPageLoaded(txnPath, TransactionPage);

export default EnhancedTransactionPage;
```

#### 函數簽名

- `withTxnPageLoaded(txnPath: string, pageComponent: React.Component) => React.Component`

#### 參數

- `txnPath`（必需）：交易路徑，用於向服務器發送請求，確保交易的有效性。

- `pageComponent`（必需）：交易頁面組件，通常是使用 `React.lazy` 延遲加載的。

#### 功能和流程

- `withTxnPageLoaded` 高階元件接受交易路徑 `txnPath` 和交易頁面組件 `pageComponent` 作為參數，然後返回一個新的 React 組件 `WithTxnPageLoaded`。

- `WithTxnPageLoaded` 組件執行以下操作：

    1. 發送與服務器的通信：組件渲染後，它會向服務器發送請求以驗證交易的有效性，前提是交易路徑 `txnPath` 存在。

    2. 處理服務器響應：處理服務器的響應，如果響應成功，則設置相關資料，否則處理錯誤並設置錯誤狀態。

    3. 延遲加載交易頁面：使用 `withLoadable` 高階元件對 `pageComponent` 進行延遲加載，以確保僅在需要時才加載交易頁面。

    4. 處理錯誤：如果發生錯誤，`WithTxnPageLoaded` 組件使用錯誤邊界來處理錯誤，確保交易頁面不會因錯誤而崩潰。

    5. 交易暫停（可選）：如果服務器返回指示交易暫停的響應，則組件會處理交易暫停並顯示相應錯誤，防止用戶繼續進行交易。

#### 示例

在上述示例中，設定了交易路徑 `txnPath` 和交易頁面組件 `TransactionPage`，然後使用 `withTxnPageLoaded` 高階元件將它們包裝在一起。這確保了在載入交易頁面之前執行必要的準備工作，包括與服務器的通信、錯誤處理以及交易頁面的延遲加載。這對確保交易頁面的安全性、可靠性和性能至關重要。

<div style='page-break-before: always; height: 0; width: 0;'></div>

### [<ins>withWrappedByDiv 高階元件</ins>](#%E7%9B%AE%E6%AC%A1)

`withWrappedByDiv` 是一個高階元件，它接受一個被包裹的 React 組件，並將其包裹在一個 `<div>` 元素中。這個高階組件用於添加外層的 `<div>` 包裹，通常用於應用樣式或其他外部元素。

#### 使用方式

```javascript
import React from 'react';
import withWrappedByDiv from './withWrappedByDiv';

// 將組件包裹在 <div> 中
const WrappedComponent = withWrappedByDiv(MyComponent);

export default WrappedComponent;
```

#### 函數簽名

- `withWrappedByDiv(WrappedComponent: React.Component) => (...classNames: string[]) => React.Component`

#### 參數

- `WrappedComponent`（必需）：要包裹在 `<div>` 中的 React 組件。

#### 功能

- `withWrappedByDiv` 高階元件接受一個 React 組件 `WrappedComponent` 作為參數，並返回一個新的函數。這個新的函數用於接收類名參數，然後返回一個包裹了 `WrappedComponent` 的組件。
- 包裹的組件會被渲染為一個帶有指定類名的 `<div>` 元素，這有助於應用樣式或其他外部元素。
- `RenderWrapComponent` 組件會接收 `WrappedComponent` 的所有屬性，並將其傳遞給被包裹的組件。
- 你可以在調用 `withWrappedByDiv` 時傳遞一個或多個類名作為參數，這些類名將被應用於包裹的 `<div>` 元素上。
- `RenderWrapComponent` 的顯示名稱會被設定為 `withWrappedByDiv(WrappedComponent)`，以便在調試中更容易識別。

<div style='page-break-before: always; height: 0; width: 0;'></div>

#### 示例

```javascript
import React from 'react';
import withWrappedByDiv from './withWrappedByDiv';

// 定義一個簡單的組件
const MyComponent = ({ text }) => {
  return <p>{text}</p>;
};

// 使用 withWrappedByDiv 包裹 MyComponent，並指定類名
const WrappedComponent = withWrappedByDiv(MyComponent)('my-wrapper', 'additional-class');

// 渲染包裹後的組件
const App = () => {
  return <WrappedComponent text="Hello, World!" />;
};

export default App;
```

在上面的示例中，`WrappedComponent` 會將 `MyComponent` 包裹在一個帶有類名 `'my-wrapper additional-class'` 的 `<div>` 元素中。