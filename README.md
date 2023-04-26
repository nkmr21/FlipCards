# FlipCards
カードをひっくり返すアニメーションの検証。文字が書いてあるのも一緒に回転する？
→表面の要素も張り付いたまま回転した。

伸ばしながら、回転できる？
→



```typescript
import {FontAwesome} from '@expo/vector-icons';
import React, {useCallback, useEffect, useState} from 'react';
import {Button, View, StyleSheet} from 'react-native';
import {Text} from 'react-native-elements';
import Animated, {
  useAnimatedStyle,
  useSharedValue,
  withTiming,
  Easing,
  withRepeat,
  withSequence,
  withDelay,
} from 'react-native-reanimated';
import {SafeAreaView} from 'react-native-safe-area-context';
import {
  VictoryBar,
  VictoryAxis,
  VictoryPolarAxis,
  VictoryGroup,
  VictoryArea,
  VictoryChart,
  VictoryTheme,
  Arc,
  Line,
} from 'victory-native';

export const Home: React.FC = () => {
  const progress = useSharedValue(0);

  const frontAnimatedStyle = useAnimatedStyle(
    () => ({
      opacity: progress.value <= 90 || progress.value >= 270 ? 1 : 0,
      transform: [{rotateY: `${progress.value}deg`}],
    }),
    [progress],
  );

  const backAnimatedStyle = useAnimatedStyle(
    () => ({
      opacity: progress.value > 90 && progress.value < 270 ? 1 : 0,
      transform: [{rotateY: `${progress.value - 180}deg`}],
    }),
    [progress],
  );

  const showOppsiteFace = useCallback(() => {
    if (progress.value <= 90) {
      progress.value = withTiming(180, {duration: 1000});
    } else {
      progress.value = withTiming(0, {duration: 1000});
    }
  }, [progress]);

  const data = [
    {x: 'aaa', y: 1},
    {x: 'bbb', y: 2},
    {x: 'ccc', y: 4},
    {x: 'ddd', y: 3},
    {x: 'eee', y: 4},
  ];

  const data2 = [
    {x: 'aaa', y: 1},
    {x: 'bbb', y: 2},
    {x: 'ccc', y: 4},
    {x: 'ddd', y: 3},
    {x: 'eee', y: 4},
    {x: 'fff', y: 4},
  ];
  const creatPolygon = (value: number) => {
    return [
      {x: 'aaa', y: value},
      {x: 'bbb', y: value},
      {x: 'ccc', y: value},
      {x: 'ddd', y: value},
      {x: 'eee', y: value},
      {x: 'fff', y: value},
    ];
  };

  return (
    <>
      <SafeAreaView style={{flex: 1}}>
        <View style={{alignItems: 'center', height: 500}}>
          <View>
            <View>
              <Animated.View style={[styles.card, styles.front, frontAnimatedStyle]}>
                <Text style={{color: 'white', fontSize: 48}}>CardFront</Text>
                <Text style={{color: 'white', fontSize: 24}}>Propaties</Text>
                <Text style={{color: 'white', fontSize: 24}}>Propaties</Text>

                <Text style={{color: 'white', fontSize: 24}}>Propaties</Text>
                <FontAwesome name="question" size={120} color="white" />
              </Animated.View>
              <Animated.View style={[styles.card, styles.back, backAnimatedStyle]}>
                <Text style={{color: 'black', fontSize: 48}}>CardBack</Text>
                <Text style={{color: 'black', fontSize: 24}}>Propaties</Text>
                <Text style={{color: 'black', fontSize: 24}}>Propaties</Text>
                <Text style={{color: 'black', fontSize: 24}}>Propaties</Text>
                <View>
                  <VictoryChart
                    polar
                    categories={{x: ['aaa', 'bbb', 'ccc', 'ddd', 'eee']}}
                    startAngle={90}
                    endAngle={450}>
                    <VictoryPolarAxis
                      style={{grid: {stroke: 'grey'}, axis: {stroke: 'none'}}}
                      labelPlacement="vertical"
                    />
                    <VictoryGroup colorScale={['grey']} style={{data: {fillOpacity: 0, strokeWidth: 1}}}>
                      <VictoryArea data={creatPolygon(1)} />
                      <VictoryArea data={creatPolygon(2)} />
                      <VictoryArea data={creatPolygon(3)} />
                      <VictoryArea data={creatPolygon(4)} />
                      <VictoryArea data={creatPolygon(5)} />
                    </VictoryGroup>
                    <VictoryGroup colorScale={['blue']} style={{data: {fillOpacity: 0.5, strokeWidth: 2}}}>
                      <VictoryArea data={data} />
                    </VictoryGroup>

                    {/* <VictoryPolarAxis circularAxisComponent={<Arc r={100} />} /> */}
                    {/* <VictoryPolarAxis circularAxisComponent={<Arc r={0} />} style={{grid: {stroke: () => undefined }}} /> */}
                  </VictoryChart>
                  <View style={{position: 'absolute', top: 140, left: 140}}>
                    <Text>上からテキストを重ねる</Text>
                  </View>

                  <View style={{position: 'absolute', top: 120, left: 180}}>
                    <FontAwesome name="question" size={48} color="black" />
                  </View>
                </View>
              </Animated.View>
            </View>
          </View>
        </View>
        <Button title="Flip" onPress={() => showOppsiteFace()} />
      </SafeAreaView>
      {/* <View style={{flex: 1, justifyContent: 'flex-end'}}>
        <Animated.View
          style={[
            {
              width: '100%',
              // height: 100,
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
      </View> */}
    </>
  );
};

const styles = StyleSheet.create({
  card: {
    width: 300,
    height: 500,
    position: 'absolute',
    left: -150, // 中心からの差分を入力する？
  },
  front: {
    backgroundColor: 'blue',
    backfaceVisibility: 'hidden',
  },
  back: {
    backgroundColor: 'yellow',
  },
});
```
