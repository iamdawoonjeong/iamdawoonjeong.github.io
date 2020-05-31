---
layout: single
title: "[HIVE] HIVE word count + 하둡 설치 실패기"
date: 2020-05-31 17:44:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- HIVE
tags:
- database
- HADOOP
- HIVE
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/hive-word-count/"
---

하둡 책 기본서를 읽어봤다면 만날수 있는 word count.  
책으로 소스만 접했을 때에는 음~해볼만할 것 같은데 했다가, 하둡 설치하는 것에서 실패.  
아니 세상에 집에다가 하둡 설치하신 분들 무슨일이지??  
윈도우 pc에 우분투 설치, vm ware 설치, vm ware 에 centos설치 까지 따라하다가 어디 선가 길을 잃었다.  
사실 이것도 몇 주전에 시도했던거라 다시 시도해 봐야지 했는데 빠른 시일내에 안할 것 같은 예감에 정리해 둔다. 벌써 가물가물...  
언제고 다시 시도 해 봐야지..  
실패하니 PC 더럽혀진 기분, 포맷하고 싶다.

<!--excerpt_separator-->


# 윈도우에 하둡 설치하기
## 1. 윈도우 store에서 검색 -> ubuntu 설치

- power shell 관리자모드로실행

```shell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
- 재부팅후 ubuntu 실행
- 사용자 ID/PW 설정


## 2. vmware player 다운로드  
<https://www.vmware.com/kr/products/workstation-player/workstation-player-evaluation.html>

## 3. centos 다운로드
<https://www.centos.org/>

### vmware player에서 centOS IOS 실행
<https://www.pawanbahuguna.com/section-packages-does-not-end-with-end-pane-dead-error-centos8/>


## Word Count
만약에 하둡 설치 성공했었더라면 한 번은 짜봤을 하둡 맵리듀스를 이해할 수 있는 wordcount 예제.  


```java
package org.myorg;

import java.io.IOException;
import java.util.*;

import org.apache.hadoop.fs.Path;
import org.apache.hadoop.conf.*;
import org.apache.hadoop.io.*;
import org.apache.hadoop.mapreduce.*;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;

public class WordCount {

 public static class Map extends Mapper<LongWritable, Text, Text, IntWritable> {
    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
        String line = value.toString();
    StringTokenizer tokenizer = new StringTokenizer(line);
    while (tokenizer.hasMoreTokens()) {
        word.set(tokenizer.nextToken());
        context.write(word, one);
    }
    }
 }

 public static class Reduce extends Reducer<Text, IntWritable, Text, IntWritable> {

    public void reduce(Text key, Iterable<IntWritable> values, Context context)
      throws IOException, InterruptedException {
        int sum = 0;
    for (IntWritable val : values) {
        sum += val.get();
    }
    context.write(key, new IntWritable(sum));
    }
 }

 public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();

    Job job = new Job(conf, "wordcount");

    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);

    job.setMapperClass(Map.class);
    job.setReducerClass(Reduce.class);

    job.setInputFormatClass(TextInputFormat.class);
    job.setOutputFormatClass(TextOutputFormat.class);

    FileInputFormat.addInputPath(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));

    job.waitForCompletion(true);
 }

}
```


---
##### References
<https://cwiki.apache.org/confluence/display/HADOOP2/WordCount>  
<https://velog.io/@lej7122/2019-06-20-1606-%EC%9E%91%EC%84%B1%EB%90%A8-7rjx4cc1e2>  
