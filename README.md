# FSharp.Compiler.Service API documentation generation

https://fsharp.github.io/FSharp.Compiler.Service

## Contributing to Library Content

To improve the content of the FSharp.Compiler.Service library documentation, contribute to the XML `///` documentation in the
signature files (`*.fsi`) in the FSharp.Compiler.Service implementation.

* Fork and clone https://github.com/dotnet/fsharp locally, see below

* Contribute to [the src/fsharp directory](https://github.com/dotnet/fsharp/tree/master/src/fsharp) and submit work to  `main` branch of https://github.com/dotnet/fsharp

* Once accepted your work will be published through a rebuild here, so submit a dummy pull request here

## Contributing to Generation of API Docs

The docs are generated by using `fsdocs` tool from FSharp.Formatting.  If you want to improve the generation process:

* Contribute to the API Docs mode and/or HTML generator in [FSharp.Formatting.ApiDocs](https://github.com/fsprojects/FSharp.Formatting/tree/master/src/FSharp.Formatting.ApiDocs) and [the `fsdocs` tool](https://github.com/fsprojects/FSharp.Formatting/tree/master/src/FSharp.Formatting.CommandTool) 

* Use a local copy of these, see below, as a subdirectory of FSharp.Compiler.Service

* Submit work to https://github.com/fsprojects/FSharp.Formatting

* Once accepted the new tooling will be published through a rebuild here, so submit a dummy pull request here that increments dummyVersion.txt

## Contributing to Layout and Design

These pages are currently using [the default template of the FSharp.Formatting tools](https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/_template.html)
with its small amount of corresponding [CSS and JavaScript](https://github.com/fsprojects/FSharp.Formatting/tree/master/docs/content)

See [FSharp.Formatting styling](https://fsprojects.github.io/FSharp.Formatting/styling.html) for information on styling for output generated by `fsdocs`.

This template is *not* the long term plan (unless it is improved enough).  We can improve the design - please help with this.  

1. Copy the default template and CSS to `docs`.  Rebuild as before.  This  template will be used instead of the default template.

2. After you have identified fixes and improvements, contribute back to the default template of FSharp.Formatting, or submit your work here and we can assess that.  This will help improve many F# libraries.

Whatever improvements you make should eventually get copied across back into FSharp.Formatting (and the duplicated template and styling will then likely be removed from this repo once it's no longer needed). If the design diverges to be a completely different look and feel then we can make several templates available in FSharp.Formatting with this as one of them.

## Build steps

Eventually the build will just be

    dotnet tool restore
    dotnet restore FSharp.Compiler.Service
    dotnet fsdocs build

For now, we make a fresh build of FSharp.Compiler.Service.

    (start in 'FSharp.Compiler.Service')
    dotnet restore FSharp.Compiler.Service

    (make 'FSharp.Compiler.Service/fsharp')
    git clone https://github.com/dotnet/fsharp --depth 1 -b main

    (build 'FSharp.Compiler.Service/fsharp')
    pushd fsharp
    .\build -noVisualStudio
    popd

Then do iterative development using:

    (from 'FSharp.Compiler.Service')
    dotnet fsdocs watch --sourcefolder fsharp  --input fsharp/docs/fcs

## CI Pipeline

This repo is published via GitHub Actions. On each push to master, the docs are built, and the outputs (which are written to the `output` directory by fsdocs) are pushed to the `gh-pages` branch. This repo is configured to host using GitHub Pages from this branch, so once the generated files are pushed the update is nearly-instant.

To build the very latest and freshest docs using the latest `fsdocs` tooling the CI does this:

1. build dotnet/fsharp `main` branch (where we assume latest doc updates have been pushed)

2. Uses the `fsdocs` tool to build the docs for the FSharp.Compiler.Service built in step 1
