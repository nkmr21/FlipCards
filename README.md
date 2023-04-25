# FlipCards
カードをひっくり返すアニメーションの検証。文字が書いてあるのも一緒に回転する？



```typescript

import React, {useEffect, useState} from 'react';
import {Button, View} from 'react-native';
import {Text} from 'react-native-elements';
import Animated, {useAnimatedStyle, useSharedValue, withTiming, Easing} from 'react-native-reanimated';
import { SafeAreaView } from 'react-native-safe-area-context';

export const Home: React.FC = () => {
  const [state, setState] = useState(false);
  const variableHight = useSharedValue(50);
  const config = {
    duration: 500,
    erasing: Easing.bezier(0.5, 0.01, 0, 1),
  };
  const style = useAnimatedStyle(() => {
    return {height: withTiming(variableHight.value, config)};
  });

  useEffect(() => {
    variableHight.value = state ? 750 : 300;
  }, [state, variableHight]);
  return (
    <>
      <SafeAreaView style={{flex: 1}}>
        <Text>TEST2</Text>
        <Button
          title="alert"
          onPress={() => {
            alert('alert');
          }}
        />
        <Button
          title="alert"
          onPress={() => {
            alert('alert');
          }}
        />
        <Button
          title="alert"
          onPress={() => {
            alert('alert');
          }}
        />
        <Button
          title="alert"
          onPress={() => {
            alert('alert');
          }}
        />
        <Button
          title="alert"
          onPress={() => {
            alert('alert');
          }}
        />
        <Button
          title="alert"
          onPress={() => {
            alert('alert');
          }}
        />
      </SafeAreaView>
      <View style={{flex: 1, justifyContent: 'flex-end'}}>
        <Animated.View
          style={[
            {
              width: '100%',
              height: 100,
              backgroundColor: '#ffffff',
              borderTopLeftRadius: 20,
              borderTopRightRadius: 20,
              borderWidth: 3,
            },
            style,
          ]}>
          <View style={{flexDirection: 'row', justifyContent: 'space-between', padding: 30}}>
            <Text>Hanako</Text>
            <View style={{width: 100, height: 50, backgroundColor: 'yellow'}}>
              <Button
                title="toggle"
                onPress={() => {
                  setState(prev => !prev);
                }}
              />
            </View>
          </View>
          <View style={{borderTopWidth: 3, padding: 30}}>
            <Text>最新の健康スコア</Text>
            <Button
              title="alert"
              onPress={() => {
                alert('alert');
              }}
            />
            <Button
              title="alert"
              onPress={() => {
                alert('alert');
              }}
            />
            <Button
              title="alert"
              onPress={() => {
                alert('alert');
              }}
            />
            <Button
              title="alert"
              onPress={() => {
                alert('alert');
              }}
            />
            <Button
              title="alert"
              onPress={() => {
                alert('alert');
              }}
            />
            <Button
              title="alert"
              onPress={() => {
                alert('alert');
              }}
            />
          </View>
        </Animated.View>
      </View>
    </>
  );
};


```
