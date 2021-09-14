---
type: docs
title: "Bootcamp GitHub workflow"
linkTitle: "Bootcamp GitHub workflow"
weight: 020
description: >
  What the GitHub workflow looks like.
---

## About

The bootcamp workflow is a watered-down version of what the final workflow will be.

Use this page to track our work on the bootcamp workflow.

## Steps to do for real

<table class="table table-striped table-bordered table-sm ">
  <thead>
    <tr>
      <th scope="col">Step name</th>
      <th scope="col">When</th>
      <th scope="col">Bootcamp workflow</th>
      <th scope="col">Notes</th>
      <th scope="col">Current status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <!-- Step name         --><td>Git pull</td>
      <!-- When              --><td>PR, main</td>
      <!-- Bootcamp workflow --><td>Same as real</td>
      <!-- Notes             --><td>Does this really apply for GitHub?</code></td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
    <tr>
      <!-- Step name         --><td>Unit tests</td>
      <!-- When              --><td>Push, PR, main</td>
      <!-- Bootcamp workflow --><td>Same as real</td>
      <!-- Notes             --><td></code></td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
    <tr>
      <!-- Step name         --><td>Build</td>
      <!-- When              --><td>PR, main</td>
      <!-- Bootcamp workflow --><td>Same as real</td>
      <!-- Notes             --><td>For SPA, do nothing because the Stage step does it<br/>For backend, build container image</code></td>
      <!-- Current status    --><td>SPA: ✔️ Done<br/>Backend: ☐ Not started </td>
    </tr>
    <tr>
      <!-- Step name         --><td>Stage</td>
      <!-- When              --><td>PR</td>
      <!-- Bootcamp workflow --><td>Same as real</td>
      <!-- Notes             --><td>For SPA, <code>uses: Azure/static-web-apps-deploy@v1</code></td>
      <!-- Current status    --><td>SPA: ✔️ Done<br/>Backend: ☐ Not started </td>
    </tr>
    <tr>
      <!-- Step name         --><td>Deploy</td>
      <!-- When              --><td>main</td>
      <!-- Bootcamp workflow --><td>Same as real</td>
      <!-- Notes             --><td>For SPA, <code>uses: Azure/static-web-apps-deploy@v1</code></td>
      <!-- Current status    --><td>SPA: 🚧 In progress<br/>Backend: ☐ Not started </td>
    </tr>
    <tr>
      <!-- Step name         --><td>Provider: Tag Pacts</td>
      <!-- When              --><td>PR, main</td>
      <!-- Bootcamp workflow --><td>Same as real</td>
      <!-- Notes             --><td></code></td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
  </tbody>

</table>

## Steps to fake for bootcamp

Just do nothing and display a success message.

<table class="table table-striped table-bordered table-sm ">
  <thead>
    <tr>
      <th scope="col">Step name</th>
      <th scope="col">When</th>
      <th scope="col">Current status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <!-- Step name         --><td>Consumer: Create/update Pacts</td>
      <!-- When              --><td>PR, main</td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
    <tr>
      <!-- Step name         --><td>Provider: Validate Pacts</td>
      <!-- When              --><td>PR, main</td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
    <tr>
      <!-- Step name         --><td>Tag</td>
      <!-- When              --><td>main</td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
    <tr>
      <!-- Step name         --><td>Static code analysis</td>
      <!-- When              --><td>PR, main</td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
    <tr>
      <!-- Step name         --><td>Integration tests</td>
      <!-- When              --><td>PR, main</td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
    <tr>
      <!-- Step name         --><td>Component tests</td>
      <!-- When              --><td>PR, main</td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
    <tr>
      <!-- Step name         --><td>Publish release notes</td>
      <!-- When              --><td>main</td>
      <!-- Current status    --><td>☐ Not started</td>
    </tr>
  </tbody>

</table>