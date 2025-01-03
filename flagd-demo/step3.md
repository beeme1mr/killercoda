We will now simulate what your application would do to retrieve a flag value.

Open a new tab (click the `+`{{}} icon near the top of the right hand panel) and run this command:

```
curl -X POST {{TRAFFIC_HOST1_8013}}/schema.v1.Service/ResolveString \
  -H "Content-Type: application/json" \
  -d '{"flagKey": "headerColor", "context": {} }'
```{{exec}}

This should return `red` because the `defaultVariant` is set to `red` in Git ([see here]({{TRAFFIC_HOST1_3000}}/openfeature/flags/src/branch/main/example_flags.flagd.json#L96)).

## Change Flag Color

Using GitOps, change the `defaultVariant` from `red` to `yellow`:

Open the Editor and find this file: `~/flags/example_flags.flagd.json`{{}}

Change the `defaultVariant`{{}} (line `96`{{}}) from `red`{{}} to `yellow`{{}}.

Change back to Tab 2 and commit these changes to your Git repository by clicking this text:

```
cd ~/flags
git add example_flags.flagd.json
git commit -m "update header color"
git push
```{{exec}}

[Line 96]({{TRAFFIC_HOST1_3000}}/openfeature/flags/src/branch/main/example_flags.flagd.json#L96) should now be `"defaultVariant": "yellow",`

## Retrieve the Flag Value Again

This time you should receive `yellow`.

```
curl -X POST {{TRAFFIC_HOST1_8013}}/schema.v1.Service/ResolveString \
  -H "Content-Type: application/json" \
  -d '{"flagKey": "headerColor", "context": {} }'
```{{exec}}
