# react-native-file-share-intent

Adds the application to the share intent of the device, so it can be launched from other apps and receive data from them 


## Installation

* Install the module

```bash
npm i --save react-native-file-share-intent
```

### Automatic Installation (React Native 0.36 - 0.59.9)

At the command line, in the project directory:

```bash
react-native link
```



## Example

### For Android

App.js

```javascript
import React, { Component } from 'react';
import  {Text,View} from 'react-native';

import RNFileShareIntent from 'react-native-file-share-intent';
 
export default class App extends Component {
  constructor(props) {
    super(props); 
    this.state = {
      fileUrl: null,
    };
  }
 
  componentDidMount() {
   if(RNFileShareIntent){
     RNFileShareIntent.getFilepath((url) => {
       this.setState({ fileUrl: url }); 
       })  
   }
  
  }
  render() {
    var uri = this.state.fileUrl;
    return (
      <View style={{flex:1,justifyContent:'center'}}>
        <Text>Shared Url: {uri}</Text>
      </View>
    );
  }
}
 
```

### For IOS Share Extension View

Share.js in the Root Folder

```javascript
import React, { Component } from 'react';
import { View, Text, AppRegistry, StyleSheet, Button } from 'react-native';
import RNFileShareIntent from 'react-native-file-share-intent';
export default class Share extends Component {
    constructor(props) {
        super(props);
        this.state = {
            sharedText: null
        };
    }
    componentDidMount() {
        var that = this;
        RNFileShareIntent.getFilePath((text) => {
            that.setState({ sharedText: text });

        })
    }

    render() {
        var url = this.state.sharedText;
        return (
            <View style={{ flex: 1, justifyContent: 'center' }}>
                <Text style={styles.text}>Shared file Path: {url}</Text>
                <Button
                    title="open With Other App"
                    color="#841584"
                    onPress={() => RNFileShareIntent.openURL(url)}
                />
                <Button
                    title="Close Extension"
                    color="#841584"
                    onPress={() => RNFileShareIntent.close()}
                />
            </View>
        )
    }
}

const styles = StyleSheet.create({
    text: {
        color: 'black',
        backgroundColor: 'white',
        fontSize: 30,
        margin: 80
    }
});

AppRegistry.registerComponent('Share', () => Share);

```



Or check the "example" directory for an example application.


## Credits

Sponsored and developed by Ajith A B
