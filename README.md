digraph G {
    label="图1 基于边缘智能与因果分析的重型车辆行驶态势分析技术路线图";
    labelloc=t;
    fontsize=16;
    rankdir=TB;
    node [shape=box, style="rounded,filled", fillcolor=lightgrey];

    subgraph cluster_1 {
        label="模块一：多场景货车刹车动力学建模与轨迹算法研发";
        style=filled;
        color=lightblue;
        A1 [label="路侧激光雷达获取数据"];
        A2 [label="道路交通视频数据"];
        B1 [label="数据清洗与标注"];
        B2 [label="数据清洗与标注"];
        C [label="基于LSTM的轨迹预测\n（嵌入刹车距离约束）", fillcolor=lightgreen];
        A1 -> B1;
        A2 -> B2;
        B1 -> C;
        B2 -> C;
    }

    subgraph cluster_2 {
        label="模块二：多源异构数据融合与边缘协同预警系统设计";
        style=filled;
        color=lightblue;
        D1 [label="路侧激光雷达数据"];
        D2 [label="道路交通视频数据\n（恶劣天气处理）"];
        D3 [label="道路传感器数据\n（ETC/气象/路面）"];
        E [label="多源数据时空对齐\n（统一时空基准）", fillcolor=lightgreen];
        F [label="边缘端实时融合\n（车速/载重/能见度）", fillcolor=lightgreen];
        D1 -> E;
        D2 -> E;
        D3 -> E;
        E -> F;
    }

    C -> F [lhead=cluster_2];

    subgraph cluster_3 {
        label="模块三：边缘智能驱动的轻量化高精度货车分类识别";
        style=filled;
        color=lightblue;
        G1 [label="基于LSTM的轨迹预测模型"];
        G2 [label="货车异常状态分类模型"];
        H [label="模型参数调优", fillcolor=lightgreen];
        I [label="模型剪枝与量化压缩\n（延迟≤20ms，准确率≥95%）", fillcolor=yellow];
        J1 [label="轻量化/高性能轨迹预测"];
        J2 [label="轻量化/高性能异常分类"];
        G1 -> H;
        G2 -> H;
        H -> I;
        I -> J1;
        I -> J2;
    }

    F -> G1;
    F -> G2;

    subgraph cluster_4 {
        label="模块四：违规行为因果建模与事故链推演";
        style=filled;
        color=lightblue;
        K1 [label="算法监测轨迹异常\n（超速/急刹/变道）"];
        K2 [label="算法监测状态异常\n（超限/载重异常）"];
        L [label="违规行为因果图模型\n（贝叶斯网络）", fillcolor=lightgreen];
        M1 [label="可解释违规判定\n（违规成因分析）"];
        M2 [label="事故风险概率推演\n（连锁反应模拟）"];
        K1 -> L;
        K2 -> L;
        L -> M1;
        L -> M2;
    }

    J1 -> K1;
    J2 -> K2;
    J1 -> K2;
}
