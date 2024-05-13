DNS Lookup
A simple browser-based tool to perform DNS lookups. Type a domain, search, and instantly get results.


SPF Explainer
A tool that explains a domain's SPF records. Search a domain and either explore its records or evaluate an IP for mail sending.

Development/Building
To setup the build/develop environment, you will need to run npm i with Node 12+ installed. This will install the dependencies to allow you to build the project.

To develop for the DNS tool run npm run dev:tools:dns-lookup, and to develop for the SPF explainer run npm run dev:tools:spf-explainer.
This will start a development server that will automatically reload the codebase when changes occur.

If you wish to host these tools on a service, simply run npm run build. This will run all the necessary build scripts automatically to build all the tools present in the source folder.
You can then take the dist folder and put it on your web server/bucket. The dist folder will contain the folders dns-lookup and spf-explainer which will each have their respective tools inside.

GitHub Actions is setup to do this automatically for this repository to deploy to gh-pages. It is also configured to deploy each PR commit to DigitalOcean Spaces for PR previews.

Source Structure
src
All the source for the tools is located within the src directory.

In this directory, there is the src/shared directory which contains centralised assets and source for the tools, such as the main Community styling which is located in src/shared/scss and the generic templates used by all tools in src/shared/templates.

Within this directory are also the main tool source directories (src/dns-lookup & src/spf-explainer).
These directories contain the specific source for that tool, which includes custom templates and style inheritance from the centralised styles.

Anything that is data which is used in a tool should be stored in src/<tool name>/data. Any helper functions should be stored in src/<tool name>/utils. Vue templates should be stored in src/<tool name>/templates with a name that makes sense for what it does. The src/<tool name>/index.html file should only be used to handle basic head information and initialise the app.

build
The build directory contains all the scripts needed to successfully build the tools into a minimal number of assets.

build/cleanDist.js is a simple script that creates the dist directory if it does not exist and then ensures that it is completely empty so that the build script has a fresh beginning.

build/fetchTemplate.js handles pulling down the blank DigitalOcean Community template page, converting it to be a PostHTML-Extend template and save it to build/base.html.

build/buildSVGs.js takes all SVG files located in src/shared/assets and converts them to JS strings (saved to build/svg/<name>.svg.js) that allow Vue/Parcel to include the SVGs inline.

build/buildTool.js is the main script file for the build process a tool in src. This builds out the mount.js file first, then compiles the scss/style.scss file to style.css, both using Parcel. Finally, the script uses PostHTML to bundle the index.html file, making use of the generate DigitalOcean Community template at build/base.html.

Contributing
If you are contributing, please read the contributing file before submitting your pull requests.

Thanks
Thanks to Cloudflare for their great WHOIS/DNS-over-HTTPS APIs. You can learn more about the importance of DNS-over-HTTPS and how to use it here.

Thanks to Matthew Gall for his wonderful WHOIS API.
