# Service Sequence Diagrams

Apply these rules when an artifact describes a software service that is being designed, implemented, or changed. These rules add to the shared contracts in `SKILL.md`.

## Required Artifact Set

1. Search the working scope for an existing sequence diagram of the service.
2. If no sequence diagram exists, tell the user that the service description requires one and ask for confirmation before creating it. Proceed without another question when the user has already authorized its creation.
3. Write each sequence diagram in PlantUML source format (`.puml`).
4. Render a PNG file (`.png`) beside each PlantUML source file. Use the same basename for the source and image.
5. Keep both the PlantUML source and PNG image as final artifacts. Do not substitute Mermaid, SVG, PDF, or another format.

If PlantUML, Java, fonts, or another rendering dependency is missing, identify the missing dependency and ask the user for permission to install it. After approval, install what is needed, generate the PNG, and continue validation. If installation is not approved, report that the required artifact set is blocked. Do not claim completion without the rendered PNG.

## Service Scope

- Make the described service the focus of the diagram.
- Cover every endpoint of the described service without exception, including public, internal, administrative, and health endpoints.
- Name every HTTP method and path explicitly. A shared flow can cover multiple endpoints only when every endpoint is named and the interaction is genuinely the same.
- Derive endpoint coverage from verified sources such as route definitions, an OpenAPI specification, or an agreed service contract. Do not infer missing endpoints.
- Show another service as a black-box participant. Show only the request, response, and externally visible failure behavior that affects the described service.
- Do not show the internal components, database operations, or internal control flow of another service, even when that implementation is known.

## Route Analysis and Lifecycle Views

Classify each route independently. Do not assign `AS-IS` or `TO-BE` once for the whole service.

Before drawing a route, record these fields in a route inventory:

| Field | Required content |
|---|---|
| Route | HTTP method and path |
| Current implementation | Verified current participants, calls, order, branches, responses, and errors |
| Planned changes | Exact planned differences for this route, or `No change` |
| Lifecycle view | `TO-BE` when planned changes exist; otherwise `AS-IS` |
| Evidence | Code locations, OpenAPI operation, or agreed contract used for verification |

When the requested plan or architecture artifact can contain this inventory, include it there. Otherwise use the inventory as temporary validation data and do not create an unrequested sidecar artifact.

Process every route in this order:

1. Describe its current implementation.
2. Record the planned changes for that route.
3. If planned behavior differs from current behavior, place the route only in the `TO-BE` view.
4. If no planned behavior differs, place the route only in the `AS-IS` view.

Each route appears in exactly one lifecycle view. Do not copy an unchanged route into `TO-BE`. Do not keep the current version of a changed route in the final `AS-IS` view.

For a service created from zero, classify every new route as `TO-BE`. Do not create an empty or speculative `AS-IS` view.

Create files only for non-empty views. Label each view clearly in the diagram title and filename. Use matching source and image names, for example `sequence-as-is.puml` with `sequence-as-is.png`, and `sequence-to-be.puml` with `sequence-to-be.png`.

## Editing and Validation

- After every PlantUML source edit, regenerate the matching PNG from the final source.
- Preserve the artifact's reader-facing content rules. Do not add review dialogue, process narration, revision notes, change summaries, `TODO`, or `TBD` text to the source or image.
- Remove superseded diagram variants and renderer byproducts after validation. Preserve user-created files when ownership is unclear.
- Open the PlantUML source and the PNG. Verify that both are readable and represent the same final content.
- Verify endpoint coverage against the route inventory. Confirm that every endpoint appears in exactly one lifecycle view.
- Check that labels are legible, content is not clipped, lifecycle status is explicit, and external services remain black boxes.
- When code exists, treat the checked-out code as the current implementation unless the user defines another baseline.
- Verify every `AS-IS` flow against the code. Check the route, participants, call order, branches, responses, and errors. Fix the diagram when it does not match the implementation.
- Compare every `TO-BE` flow with the current code and the recorded planned changes. Confirm that the diagram contains at least one planned difference that is not already implemented.
- If a `TO-BE` flow already matches the current code, reclassify it as `AS-IS` when no further change is planned. Otherwise correct the `TO-BE` flow so it represents the actual planned difference.
- Reclassify a former `TO-BE` flow as `AS-IS` after its planned behavior exists in the selected current-code baseline.
- Fix every problem, render again, and repeat the complete check.
