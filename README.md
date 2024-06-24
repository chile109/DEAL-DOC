## Docfx quick start
https://dotnet.github.io/docfx/
Make sure you have .NET SDK installed, then open a terminal and enter the following command to install the latest docfx:

```
dotnet tool update -g docfx
```
To create a new docset, run:

```
docfx init
```
This command walks you through creating a new docfx project under the current working directory. To build the docset, run:

```
docfx docfx.json --serve
```
Now you can preview the website on http://localhost:8080.

To preview your local changes, save changes then run this command in a new terminal to rebuild the website:

```
docfx docfx.json
```

## Update API flow
1. Add xml description for public method.
2. Copy `MustaverseLab.DEAL.Runtime.csproj` to root folder.
3. Run `docfx docfx.json --serve` in terminal and check in http://localhost:8080.
4. Commit and push changes to branch `docfx`
5. CI action will auto run depoly.
6. Check on https://chile109.github.io/DEAL-DOC/api/index.html

## Reference
https://github.com/NormandErwan/DocFxForUnity