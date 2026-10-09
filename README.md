# Tally SDK assessment

I used Voxgig's SDK generator to try building a TypeScript SDK for Tally's forms API. The goal was to generate the SDK, run its tests and use it to retrieve a test form I had created.

## Where I stopped

I scaffolded the project and installed its dependencies manually after automatic installation failed. Generation then ran into file lookup errors. One troubleshooting attempt reached OpenAPI parsing and started generating TypeScript files, but it did not finish.

I haven't verified the SDK build, run its tests or made a live API request. I prepared the report and repository afterwards.

## Report

[Read the assessment report](REPORT.md) for the steps I took, the errors I encountered, suggested improvements and how I used AI.

## Files

The `.sdk` folder contains the generator setup, OpenAPI specification and models. Any TypeScript files generated during the attempt are incomplete and unverified.