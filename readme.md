# Walkthough
## Create the new project
- pac pcf init --namespace DTS --name DTSIFrameSandbox --template field
- npm i
## Add sanitizer for the styles and iframe parameters
- npm i dompurify --save
- npm i --save-dev @types/dompurify
## Change predefined manifest file
- version="0.0.1" > version="1.0.0"
- description-key="DTSIFrameSandbox description" > description-key="DTS Power Apps Custom Framework component to add an sandboxed IFrame to Apps. Style, src and srcdoc are parameterized."
- remove <property name="sampleProperty" display-name-key="Property_Display_Key" description-key="Property_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" />
- add <property name="iframestyles" display-name-key="IFrame Styles" description-key="CSS description of #wrap and #frame placed DOMPurified between style tags in the component" of-type="SingleLine.Text" usage="bound" required="true" />
- add <property name="iframesrc" display-name-key="IFrame src" description-key="Optional URL for the iFrame sandbox tag" of-type="SingleLine.Text" usage="bound" required="false" />
- add <property name="iframesrcdoc" display-name-key="IFrame srcdoc" description-key="Optional content for the iFrame sandbox tag." of-type="SingleLine.Text" usage="bound" required="false" />
- run npm run build to update the types.d.ts
## Develop the code in index.ts
- see code
- test in browser: npm start
## Package components
- Create folder Solutions
- Navigate to folder Solutions
- pac solution init --publisher-name dts --publisher-prefix dts 
## Update Solution.xml
- <UniqueName>solutions</UniqueName> > <UniqueName>DTSIFrameSandbox</UniqueName>
- <LocalizedName description="solutions" languagecode="1033" /> > <LocalizedName description="DTSIFrameSandbox" languagecode="1033" />
- SKIP, AS DOES NOT BUILD: <Managed>2</Managed> > <Managed>1</Managed>
- pac solution add-reference --path D:\Data\2021\20210524IFrameSandboxPCF
- & 'C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\MSBuild\Current\Bin\MSBuild.exe' /t:restore
- & 'C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\MSBuild\Current\Bin\MSBuild.exe'
- Import v1.0.0
