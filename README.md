## 项目实现方案：GBM综合数据库（OrganoGBM）

### 一、数据库设计（MySQL）

#### 数据库：`OrganoGBM`

- 表设计：
  1. **细胞器基因表（organelle_genes）**
     - gene_id (主键)
     - gene_name
     - organelle_type

  2. **差异基因表（deg）**
     - gene_id (外键)
     - logFC
     - p_value
     - adj_p_value

  3. **突变信息表（mutations）**
     - mutation_id
     - gene_id (外键)
     - mutation_type
     - amino_acid_change
     - position

  4. **CNV信息表（cnv）**
     - gene_id (外键)
     - sample_id
     - cnv_value

  5. **临床信息表（clinical_info）**
     - sample_id
     - patient_id
     - age
     - gender
     - survival_status

### 二、后端实现（Python + Flask）

- 后端框架：Flask
- 接口实现：
  - 基因搜索功能：输入细胞器名称，查询并返回基因列表。
  - 差异基因交集功能：后端实现两个表的基因交集运算，返回特定细胞器差异基因列表。
  - 数据查询与传输API：突变信息、CNV相关性分析、临床信息与PubMed查询。
  - KEGG API调用接口：返回相关基因的富集通路数据。

### 三、前端实现（Vue.js）

- 前端框架：Vue.js + Element UI
- 交互组件：
  - 搜索框与下拉菜单选择细胞器。
  - 可交互火山图（使用echarts.js或Plotly）。
  - 火山图点击点事件，跳转到突变信息的棒棒糖图及CNV相关性分析图页面。
  - PubMed文献热度展示。

### 四、可视化实现（R）

- 火山图制作：ggplot2/plotly实现交互式火山图。
- 突变棒棒糖图：maftools或trackViewer。
- CNV分析：ggplot2绘制CNV相关性分析图。
- KEGG富集通路分析：clusterProfiler包。

### 五、PubMed API整合
- 使用Entrez Direct或NCBI的REST API获取文献信息和研究热度。

### 六、网站部署与集成
- 后端部署：Docker容器部署于云服务器
- 前端部署：Nginx静态资源管理
- 数据库：MySQL容器化部署

