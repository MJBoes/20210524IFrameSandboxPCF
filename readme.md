![](https://github.com/MJBoes/20210524IFrameSandboxPCF/blob/master/ReadmeAssets/Screenshot%20Component.png)
# Summary
This project adds a simple iFrame functionality to Canvas Power Apps. It is primarily intended to display HTML pages constructed from the Power Automate Flow Designer, but can be used for other needs as well.
## Example
The Canvas App in the screenshot contains the control with the name dtsFlowViewer and is configured as follows:
~~~~
iframestyles="#dtswrap {width: " & dtsFlowViewer.Width & "px;height: " & dtsFlowViewer.Height & "px;padding: 0;overflow: hidden;border:1px solid #00126B;} #dtsiframe { width: " & 100/sldZoom.Value*100 & "%; height: "& 100/sldZoom.Value*100 & "%; border: none; transform: scale(" & sldZoom.Value / 100 & "); transform-origin: 0 0;}"
iframesrcdoc=varSourceDoc
~~~~
The slider is called sldZoom and by updating the iframesstyle parameter, the content in the iFrame is scale when the zoom percentage is changed.
The varSourceDoc just contains the HTML to be displayed.
## Script attack mitigation
The component has two defences against malicious usage. The HTML inserted in the iFrame element is sanitized first with DOMPurify. Also, the iFrame tag as the sandbox attribute applied.

# Walkthough
## Create the new project
- pac pcf init --namespace DTS --name DTSIFrameSandbox --template field
- npm i
## Add sanitizer for the styles and iframe parameters
- npm i dompurify --save
- npm i --save-dev @types/dompurify
## Change predefined manifest file
~~~
- version="0.0.1" > version="1.0.0"
- description-key="DTSIFrameSandbox description" > description-key="DTS Power Apps Custom Framework component to add an sandboxed IFrame to Apps. Style, src and srcdoc are parameterized."
- remove <property name="sampleProperty" display-name-key="Property_Display_Key" description-key="Property_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" />
- add <property name="iframestyles" display-name-key="IFrame Styles" description-key="CSS description of #wrap and #frame placed DOMPurified between style tags in the component" of-type="SingleLine.Text" usage="bound" required="true" />
- add <property name="iframesrc" display-name-key="IFrame src" description-key="Optional URL for the iFrame sandbox tag" of-type="SingleLine.Text" usage="bound" required="false" />
- add <property name="iframesrcdoc" display-name-key="IFrame srcdoc" description-key="Optional content for the iFrame sandbox tag." of-type="SingleLine.Text" usage="bound" required="false" />
- run npm run build to update the types.d.ts
~~~
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

## Publish to github
Some references to blog or YouTube video to follow.

## 1.0.1
Added check on src parameter to support both src and srcdoc property (src does not render if there is a srcdoc attribute)
npm run build
create sub folder v101, navigate in folder, pac solution init --publisher-name dts --publisher-prefix dts
update solution.xml
pac solution add-reference --path D:\Data\2021\20210524IFrameSandboxPCF
cd..
& 'C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\MSBuild\Current\Bin\MSBuild.exe' /t:restore
& 'C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\MSBuild\Current\Bin\MSBuild.exe'
-> version is recognized as an update over 1.0
