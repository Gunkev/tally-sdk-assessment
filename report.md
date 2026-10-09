# Tally SDK assessment report

## Preparation

I created a free Tally account, generated an API key and published a small form called "Voxgig", so I would have something recognisable to retrieve. I then downloaded the OpenAPI specification. I didn't get to use the key because SDK generation failed before I could test a live request.

## Goal and outcome

I chose Tally's forms API because it provides free API access and an official OpenAPI specification. I search for Tally in the Voxgig's public catalogue and found no repository with its name or description.

I planned to generate a TypeScript SDK, run its tests and retrieve a test form through an authenticated request.

I stopped technical work at 30 minutes. Scaffolding and manual dependency installation progressed, but SDK generation remained incomplete. I did not reach SDK build verification, tests or a live API request. This report and repository packaging were prepared afterwards.

## Environment

Windows PowerShell, Node.js 22.20.0, npm 10.9.3.

Installed packages:

- `@voxgig/apidef` 8.25.1
- `@voxgig/model` 12.0.1
- `@voxgig/sdkgen` 4.34.4
- `aontu` 0.76.0

Specification: https://developers.tally.so/api-reference/openapi.json

## Observations

### Automatic installation failed

I started with:

    npm create @voxgig/sdkgen@latest -- tally -d ./openapi.json -o ./tally-sdk -t ts -f test

The scaffolder failed during automatic installation with `Failed to start npm: spawn npm ENOENT`, although npm commands worked directly in PowerShell.

I retried the command with `--no-install` and it still failed because those options required installed dependencies. I then installed dependencies manually and added the TypeScript target and test feature.

### Generation encountered conflicting path lookups

Running `npm run generate` from `.sdk` failed to resolve `api/api-info.aontu`. I checked `model/api/api-info.aontu` with PowerShell's `Test-Path`, which returned `True`. The error's search paths did not include that location. Supplying an absolute root-file path produced the same failure.

Running the model builder from `.sdk/model` progressed through OpenAPI parsing and started TypeScript generation. However, it then searched for a test-feature template under `.sdk/model/tm` and failed.

Changing directories helped the include lookup but introduced a template lookup failure. I did not establish the underlying cause or a working fix.

The parser also reported two undeclared `organizationId` parameters, which it inferred as required strings. These warnings were separate from the error that stopped generation.

## Suggested improvements

- Check why automatic installation fails on Windows when npm works directly in PowerShell, and document the steps for installing dependencies manually.
- Make it clear that using `--no-install` means dependencies must be installed before adding targets and features.
- Check how model includes and templates are located. Changing directories let me get past one error, but caused another.
- Show which directory an include path is resolved against. This would have helped me understand why the generator couldn't find a file that was already there.

## AI use

I used ChatGPT to find documentation, help interpret errors and suggest diagnostic commands. I ran the commands and checked their outputs myself.