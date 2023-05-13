# Company.info client for server-side Google Tag Manager

## About the project
This Company.info client allows you to retrieve company details from the Company.info API in server-side Google Tag Manager (GTM). These details are made available as event data in server-side GTM and can be returned to the browser. 

Detailed instructions to configure and use this template can be found in this article: [Company.info server-side Google Tag Manager client configuration instructions](https://www.michelbieze.com/blog/company-info-template-server-side-google-tag-manager).

## Getting started
- Import the client template in server-side GTM.
- Add the Company.info client to clients. 
- Configure the fields:

    - **Request path**: Google Tag Manager pathname for this client.
    - **Allowed top level domains**: base domains that are allowed to make requests to the client, e.g. michelbieze.com or domain.com. Use * to whitelist all domains *(not recommended)*.
    - **Company.info Company Card**: API Company Card provided by Company.info.
    - **Company.info Contract Card**: API Contract Card provided by Company.info.
    - **Fields to return to browser (case sensitive)**: API fields to be returned to the browser. An empty object is returned to the browser if left empty. 

## Example to call the client from the browser
The code block contains an JavaScript example of how the client can be called from the browser. *Note:* Don't forget the update your GTM container URL and client path in the example.

```
async function getCompanyInfoData() {
  try {
    const response = await fetch('https://gtm.your-domain.com/c-info', { 
      mode: 'cors', 
      credentials: 'include' 
    })
    const data = await response.json();
    return JSON.parse(data);
  } catch (error) {
    /* handle error */
    return;
  }
};

async function logCompanyData() {
  const companyData = await getCompanyInfoData();
  if (typeof companyData !== 'object') {
    /* add fallback, API call failed */
    console.log('Company.info API call failed')
    return;
  }
  console.log('Company.info data returned by API:', companyData);
}

logCompanyData();
```

