
# Link Unfurling Investigation

## Work flow

- Add the messageHandlers array to your app manifest
```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
],
```

- Handle the composeExtension/queryLink invoke in bot endpoint
```ts
public async handleTeamsAppBasedLinkQuery(context: TurnContext, query: any): Promise<any> {
  const attachment = CardFactory.thumbnailCard('Thumbnail Card',
    query.url,
    ['https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png']);

  const result = {
    attachmentLayout: 'list',
    type: 'result',
    attachments: [attachment]
  };

  const response = {
    composeExtension: result
  };
  return response;
}
```

![link-unfurling](./link-unfurling-images/link-unfurling.png)


## App-less link unfurling
One of the features of link unfurling is the adoption of schema.org – if a URL has attached metadata as specified, Teams is able to match that to a pre-defined card template and then render a card when a link is displayed in the client. Here’s an example of how this works:

![app-less-link-unfurling-example](./link-unfurling-images/app-less-link-unfurling-example.png)

### Example of HTML with metadata:

```html
<div itemscope itemtype ="https://schema.org/Movie">
  <h1 itemprop="name">Avatar</h1>
  <div itemprop="director" itemscope itemtype="https://schema.org/Person">
  Director: <span itemprop="name">James Cameron</span> (born <span itemprop="birthDate">August 16, 1954</span>)
  </div>
  <span itemprop="genre">Science fiction</span>
  <a href="../movies/avatar-theatrical-trailer.html" itemprop="trailer">Trailer</a>
</div>
```

## Some limitations
- Currently, link unfurling is not supported on Mobile clients.
- Today link unfurling must be done in the context of a message extension app which requires a bot.
- The link unfurling result is cached for 30 minutes. (Cannot find ways to remove this cache)