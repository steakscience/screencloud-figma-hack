# Resources

## Figma file

The Figma file can be downloaded [here](resources/example_figma_template.fig), and the JSON downloaded [here](resources/calendar.json). The plugin we used during the hackathon was JSON to Figma, but any similar plugin should work fine.

To get around ScreenCloud players’ iframe limitation, we recommend putting Figma embeds inside our [example HTML file](resources/embed.html), then host it using services like Github Pages. The resulting link can be added to ScreenCloud via the Links feature.

## ScreenCloud API

We used the ScreenCloud API to switch content on our screens. In our case, we used `setScreenContentByLinkId` for simplicity, but similar calls for channels, playlists, etc should work the exact same way. More info on the API can be found on the [developer website](https://screencloud.github.io/signage-next-graphql-docs/).

```GraphQL
mutation {
  setScreenContentByLinkId(input: {
    clientMutationId: "Switch Links",
    linkId: "9b1c1755-c43f-4c9e-94a7-5f6c5710e05c",
    screenId: "f7580bf7-9605-421c-a951-9c4cf424cb5e"
  })  {
    clientMutationId
  }
}
```

Screen ID and channel/link/playlist IDs can be queried using `allChannels` (or similar), or via Studio Audit Logs.

```GraphQL
allChannels(filter: {draftOf: {isNull: true}}) {      
    nodes {
    id
    name
    }
}
```

The best use for this is to implement trigger conditions, ie. trigger content switching when we have a new error in our dashboard, etc.

This is a very compelling usecase in addition to time-based looping content.