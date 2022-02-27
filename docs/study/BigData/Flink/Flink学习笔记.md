#  Flink 学习笔记


## Flink 流处理Api

### 1 Source
#### 1.1 从集合读取数据
~~~ java
// 创建执行环境
StreamExecutionEnvironment env=StreamExecutionEnvironment.getExecutuionEnvironment();
// 从集合读取数据
DataStream<T> inputStream=env.fromCollection(Array.asList(new T(),new T(),new T()));

DataStream<Integer> integer = env.fromElements(1,2,3,4,5);
~~~
#### 1.2 从文件读取数据
~~~ java
// 创建执行环境
StreamExecutionEnvironment env=StreamExecutionEnvironment.getExecutuionEnvironment();
// 从文件读取数据
DataStream<String> inputStream=env.readTextFile("filePath");

DataStream<Integer> integer = env.readFile("filePath");
~~~

#### 1.3 从消息队列读取数据（kafka）
~~~ java
// 创建执行环境
StreamExecutionEnvironment env=StreamExecutionEnvironment.getExecutuionEnvironment();
// 从kafka读取数据
DataStream<String> inputStream=env.addSource(new FilnkKafkaConsumer())

DataStream<Integer> integer = env.readFile("filePath");
~~~

#### 1.4 自定义source
~~~ java
// 创建执行环境
StreamExecutionEnvironment env=StreamExecutionEnvironment.getExecutuionEnvironment();
// 从自定义source读取数据
DataStream<String> inputStream=env.addSource(new MySource())

//自定义source 
public static MySource() implements SourceFunction<T>{

    private runFlag=true;

    @Override
    public void run(SourceContext<T> ctx){
        while(runFlag){
            //生成自定义数据
            ctx.collect(new T);
        }

    }

    @Override
    public void cnacel(){
        runFlag=false;
    }
}
~~~