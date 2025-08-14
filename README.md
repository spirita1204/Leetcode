![LeetCode Total](https://img.shields.io/badge/LeetCode%20Solved-1010-red) ![Easy](https://img.shields.io/badge/Easy-320-green) ![Medium](https://img.shields.io/badge/Medium-587-yellow) ![Hard](https://img.shields.io/badge/Hard-103-blue) ![Acceptance Rate](https://img.shields.io/badge/Acceptance%20Rate-64.4%25-lightgrey) ![Ranking](https://img.shields.io/badge/Ranking-22062-purple)

































## LeetCode Statistics
<img src="https://leetcard.jacoblin.cool/spirita1204?theme=dark&font=Short%20Stack&ext=heatmap" alt="My LeetCode statistics" />

Automatically package the LeetCode problems written daily into an .md file through Notion using a **Zapier workflow + Webhooks** and upload it to the github.

<h3 align="left">Tools:</h3>
<p align="left"> 
  <a href="https://www.notion.com/zh-tw" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Notion-logo.svg/1200px-Notion-logo.svg.png" alt="notion" width="40" height="40"/> </a>
  <a href="https://zapier.com/l/home?utm_source=google&utm_medium=cpc&utm_campaign=gaw-gbl-nua-search-brand-remarketing&utm_term=zapier&utm_content=21098&utm_ads_campaign_id=17613359682&utm_ads_adset_id=136156400777&utm_ads_ad_id=607316261972&gad_source=1&gclid=CjwKCAiAneK8BhAVEiwAoy2HYR5IH5IRV3K59qshBJuy2OkkjfCwb1R8IvfBZOOB6XihnrbiIINeyBoClSMQAvD_BwE" target="_blank" rel="noreferrer"> <img src="https://banner2.cleanpng.com/20180805/gpt/kisspng-zapier-logo-world-wide-web-product-mobile-app-zapier-integration-verticalresponse-5b669ba2609b29.1196434715334511703957.jpg" alt="zapier" width="40" height="40"/> </a>
  <a href="https://docs.github.com/en/rest" target="_blank" rel="noreferrer"> <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRw8AHWfvfU99X7gPZDKalDYZWcC_ROQc4Fag&s" alt="github_api" width="40" height="40"/> </a> 
</p>
<img src="https://i.ibb.co/tpCQ8Yb/2025-01-28-165335.png" width="60%">
<img src="https://i.ibb.co/M1qMhrS/2025-01-28-164652.png" width="60%">

```jsx
-------------------------------
1.Run Javascript 取代標題底線
-------------------------------

// this is wrapped in an `async` function
// you can use await throughout the function
const content = inputData.content;
const replacedContent = content
  .replace(/\s+/g, '-') // 將所有空白替換為 '-'
  .replace(/\./g, '')   // 移除 '.'
  .replace(/\//g, '-'); // 將 '/' 替換為 '-'

return { result: replacedContent };

-------------------------------
2.Run Javascript 將內容 Base64 進行傳輸
-------------------------------

const content = inputData.content;
const methods = inputData.methods;
const dataStructure = inputData.dataStructure;
const diff = inputData.diff;
const similar = inputData.similar;
// Information to prepend
let combinedContent = "";
combinedContent += "# " + inputData.title + "  \n\n  ";// 標題
if(methods)
    combinedContent += "Methods: " + methods + " </br> ";
if(dataStructure)
    combinedContent += "Data Structure: " + dataStructure + " </br> ";
if(diff)
    combinedContent += "Difficulty: " + diff + " </br> ";
if(similar)
    combinedContent += "Similar: " + similar + " </br> ";
combinedContent += ("</br>" + content);
// Base64 encode the combined content
const encodedContent = Buffer.from(combinedContent).toString('base64');

return { encoded: encodedContent };

-------------------------------
3.Run Python 透過Github API 自動創建/更新文件
-------------------------------

import requests
import base64

# Define the inputData with necessary details (make sure to pass the actual data)
inputData = {
    'title': inputData['title'] ,  # Replace with the actual file title
    'encoded': inputData['encoded']  # Replace with the actual base64-encoded content
}

# URL and data placeholders
url = f"https://api.github.com/repos/spirita1204/Leetcode/contents/{inputData['title']}.md"

# Data for the request
data = {
    "message": f"Add {inputData['title']}.md file",
    "content": inputData['encoded'],  # Base64-encoded content
    "branch": "main"
}

# Authorization and headers
headers = {
    "Content-Type": "application/json",
    "Authorization": "Bearer #YOUR_AUTHORIZATION_TOKEN#",
    "X-GitHub-Api-Version": "2022-11-28"
}

# Make the PUT request to GitHub API
response = requests.put(url, json=data, headers=headers)

# Check the response
if response.status_code == 201:
    print("File created successfully!")
else:
    print(f"Error: {response.status_code}, {response.text}")
    if(response.status_code == 422): #如果是文件已存在的錯誤碼，則嘗試覆蓋文件
        # 獲取文件sha
        response = requests.get(url, headers=headers)
        if response.status_code == 200:
            sha = response.json()['sha']
            print("sha: ", sha)
            dataAddSha = {
                "message": f"Update {inputData['title']}.md file",
                "content": inputData['encoded'],  # Base64-encoded content
                "sha": sha
            }
            # 更新文件
            response = requests.put(url, json=dataAddSha, headers=headers)
            print("File updated successfully!")
        else:
            print(f"Error: {response.status_code}, {response.text}")
# Returning the result (for Zapier or further use in your code)

return {'success': 'success'}

```
