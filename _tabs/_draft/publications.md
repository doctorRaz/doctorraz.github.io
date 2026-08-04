---
layout: page
icon: fas fa-book
order: 10
---

<!-- markdownlint-disable MD033 MD041 -->

<style>
.section-title {
    font-size: 1.8rem;
    margin: 30px 0 20px 0;
    color: var(--heading-color);
    border-bottom: 2px solid var(--border-color);
    padding-bottom: 10px;
    position: relative;
}

.section-title::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 100px;
    height: 2px;
    background: var(--link-color);
}

.publication-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    margin-bottom: 30px;
}

.publication-card {
    display: flex;
    flex-direction: column;
    width: 100%;
    border: 1px solid var(--border-color);
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.3s ease;
    background-color: var(--card-bg);
    margin-bottom: 20px;
    position: relative;
}

.publication-card:hover {
    transform: translateY(-5px);
}

.publication-card:not(:last-child)::after {
    content: '';
    position: absolute;
    bottom: -10px;
    left: 50%;
    transform: translateX(-50%);
    width: 80%;
    height: 1px;
    background: linear-gradient(to right, transparent, var(--border-color), transparent);
}

.publication-info {
    padding: 15px;
}

.publication-title-container {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 10px;
}

.publication-title {
    font-size: 1.2rem;
    margin: 0;
    color: var(--link-color);
}

.publication-button {
    padding: 4px 12px;
    border-radius: 4px;
    font-size: 0.8rem;
    text-decoration: none;
    transition: background-color 0.3s ease;
}

.paper-button {
    background-color: var(--link-color);
    color: white;
}

.doi-button {
    background-color: #0070f3;
    color: white;
}

.publication-button:hover {
    opacity: 0.9;
}

.publication-abstract {
    margin: 15px 0;
    padding: 10px;
    background-color: var(--card-bg);
    border-left: 3px solid var(--link-color);
    font-size: 0.9rem;
    color: var(--text-color);
}

.publication-image-container {
    width: 100%;
    height: 200px;
    overflow: hidden;
    margin-top: 15px;
}

.publication-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.publication-authors {
    color: var(--text-color);
    margin: 0 0 8px 0;
    font-size: 0.9rem;
    font-style: italic;
}

.publication-venue {
    color: var(--text-color);
    margin: 0 0 8px 0;
    font-size: 0.9rem;
    font-weight: bold;
}

.publication-description {
    color: var(--text-color);
    margin: 0;
    font-size: 0.9rem;
}

.publication-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 15px;
}

.publication-tag {
    display: inline-flex;
    align-items: center;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.8rem;
    font-weight: 500;
    transition: all 0.3s ease;
}

.publication-tag:nth-child(1) {
    background-color: #e3f2fd;
    color: #1976d2;
}

.publication-tag:nth-child(2) {
    background-color: #f3e5f5;
    color: #7b1fa2;
}

.publication-tag:nth-child(3) {
    background-color: #e8f5e9;
    color: #2e7d32;
}

.publication-tag:nth-child(4) {
    background-color: #fff3e0;
    color: #f57c00;
}

.publication-tag:nth-child(5) {
    background-color: #fce4ec;
    color: #c2185b;
}

.publication-tag:nth-child(6) {
    background-color: #e0f7fa;
    color: #0097a7;
}

.publication-tag:nth-child(7) {
    background-color: #f1f8e9;
    color: #689f38;
}

.publication-tag:hover {
    transform: translateY(-2px);
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.section-divider {
    width: 100%;
    height: 2px;
    background: linear-gradient(to right, transparent, var(--border-color), transparent);
    margin: 40px 0;
}
</style>

<!-- Conference Section -->
<h2 class="section-title">Conference</h2>
<div class="publication-container">
  <!-- Traffic Classification Paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">Traffic Classification using Deep Learning: High Accuracy is Not Enough</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/Traffic_Classification_using_Deep_Learning.pdf" class="publication-button paper-button">Paper</a>
        <a href="https://dl.acm.org/doi/10.1145/3405837.3411369" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Kanghee Lee, Seunghun Lee, and Hyun-chul Kim</p>
      <p class="publication-venue">ACM SIGCOMM, New York City, Aug. 2020.(Poster)</p>
      <div class="publication-abstract">
        As Deep Learning (DL) algorithms have rapidly become a methodology of choice in various domains, they have recently entered also the field of the Internet traffic classification, successfully demonstrating impressive results. Most of the research work up to this point has focused on improving the accuracy of classification systems, yet there has been little attempt to provide (i) systematic comparison of the various DL algorithms used and (ii) analysis on where the higher accuracy come from, particularly when comparing with the traditional machine learning algorithms like C4.5. To fill this gap, we conduct experiments with four DL algorithms proposed for traffic classification, including CNN, LSTM, Stacked Auto-Encoder (SAE), and Hierarchical Attention Networks (HAN). Further, we propose to leverage and visualize hierarchical attention layers to highlight which parts of the traffic packet traces were most informative for accurate classification, which provides hints about why (and how) DL algorithms achieve the state-of-the-art level high accuracy. We view this paper as the first step towards answering the aforementioned "why" question, which is critical in understanding the real benefit and contribution of deep learning to the field of the Internet traffic classification, and advancing its state-of-the-art.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Deep Learning</span>
        <span class="publication-tag">Network Traffic</span>
        <span class="publication-tag">Traffic Classification</span>
        <span class="publication-tag">Explainable AI</span>
      </div>
    </div>
  </div>

  <!-- Crowdfunding Success Prediction Paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">Content-based Success Prediction of Crowdfunding Campaigns: A Deep Learning Approach</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/Content-based_Success_Prediction_of_Crowdfunding.pdf" class="publication-button paper-button">Paper</a>
        <a href="https://dl.acm.org/doi/10.1145/3272973.3274053" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Seunghun Lee, Kanghee Lee, and Hyun-chul Kim</p>
      <p class="publication-venue">ACM CSCW, New York City's Hudson River (Jersey City), Nov. 2018.(Poster)</p>
      <div class="publication-abstract">
        Despite the huge success of crowdfunding platforms, the average project success rate is 41%, and it has been decreasing. Hence, finding out the factors that lead to successful fundraising and predicting the probability of success for a project has been one of the most important challenges in the crowdfunding. This work is the first attempt to use in-band project content - text - data only, contained in all the Campaign, Updates, and Comments sections of a crowdfunding project (not in combination with any other out-of-band project metadata or statistically-derived numeric features), for success prediction. By adopting (i) the sequence to sequence (seq2seq) deep neural network model with sentence-level attention and (ii) Hierarchical Attention-based Network (HAN) model, we demonstrate that our proposed model achieves the state-of-the-art performance in predicting success of campaigns, as much as 89-91%. We also show that our method achieves 76% accuracy on average on the very first day of project launch, using campaign main text data only.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Deep Learning</span>
        <span class="publication-tag">Crowdfunding</span>
        <span class="publication-tag">Success Prediction</span>
        <span class="publication-tag">Hierarchical Attention Networks</span>
      </div>
    </div>
  </div>

  <!-- Crowdfunding scam detection Paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">The Language of Deceivers: Linguistic Features of Crowdfunding Scams</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/The_Language_of_Deceivers.pdf" class="publication-button paper-button">Paper</a>
        <a href="https://dl.acm.org/doi/10.1145/2872518.2889356" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Wafa Shafqat, Seunghun Lee, Sehrish Malik, and Hyun-chul Kim</p>
      <p class="publication-venue">International World Wide Web conference (WWW), Montreal, Canada, Apr. 2016.(Poster)</p>
      <div class="publication-abstract">
        Crowdfunding sites with recent explosive growth are equally attractive platforms for swindlers or scammers. Though the growing number of articles on crowdfunding scams indicate that the fraud threats are accelerating, there has been little knowledge on the scamming practices and patterns. The key contribution of this research is to discover the hidden clues in the text by exploring linguistic features to distinguish scam campaigns from non-scams. Our results indicate that by providing less information and writing more carefully (and less informally), scammers deliberately try to deceive people; (i) they use less number of words, verbs, and sentences in their campaign pages. (ii) scammers make less typographical errors, 4.5-4.7 times lower than non-scammers. (iii) Expressivity of scams is 2.6-8.5 times lower as well.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Linguistic Analysis</span>
        <span class="publication-tag">Crowdfunding</span>
        <span class="publication-tag">Scam Detection</span>
      </div>
    </div>
  </div>

  <!-- SNS Map Paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">SNS Map : Location-based SNS data mapping system</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/SNSMap.pdf" class="publication-button paper-button">Paper</a>
        <a href="https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE06645952" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Seunghun Lee, Daeyoung Oh, Minhyuk Kang, and Hyun-chul kim</p>
      <p class="publication-venue">한국컴퓨터종합학술대회(In Proceedings of the Korea Computer Congress(KCC)), Jeju, Korea, June. 2015.</p>
      <div class="publication-abstract">
        매일 트위터, 페이스북, 유튜브와 같은 Online Social Netowrks(OSN)에서는 하루 수억 건의 많은 메시지가 올라온다. 이 수많은 메시지 사이에서 사용자가 원하는 메시지와 정보를 효율적으로 찾기란 어려운 일이다. 이러한 이유로 좀 더 편리하고 간편하게 원하는 메시지와 정보를 찾기 위한 시스템이 만들어지고 연구가 되고 있다. 특히 맵을 통해서 수집되고 있는 데이터를 보여주는 많은 시스템이 중점적으로 만들어 지고 있다. 하지만 이 수집된 데이터를 분석까지 해서 보여주는 시스템은 거의 없다. 본 논문에서는 OSN 중에 하나인 트위터에서 PlanetLab System을 이용한 대규모 데이터를 수집하는 방법과 수집된 데이터를 맵을 통해서 보여주는 시각화, 키워드 분석을 통한 검색, 필터링 기능, Sentiment Analysis & Word Cloud를 이용한 데이터 분석을 이용해서 만든 위치기반 SNS 데이터 맵핑 시스템을 제안하고, 초기 프로토타입인 SNS Map 시스템을 구축한다.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Mapping System</span>
        <span class="publication-tag">Twitter</span>
      </div>
    </div>
  </div>
</div>

<div class="section-divider"></div>

<!-- Journal Section -->
<h2 class="section-title">Journal</h2>
<div class="publication-container">
  <!-- Fraud Detection IEEE Access Paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">Fraud Detection on Crowdfunding Platforms using Multiple Feature Selection Methods</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/Fraud_Detection_IEEEAccess.pdf" class="publication-button paper-button">Paper</a>
        <a href="https://doi.org/10.1109/ACCESS.2025.3547396" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Seung-hun Lee, Heemin Park, and Hyun-chul Kim</p>
      <p class="publication-venue">IEEE Access, March 2025</p>
      <div class="publication-abstract">
        In recent years, crowdfunding has emerged as an alternative funding source for startups and emerging businesses, experiencing significant growth. However, this growth has also led to an increase in fraudulent activities. Despite the potential for fraud in the realm of crowdfunding, there is limited knowledge of the phenomenon due to a lack of data on actual instances of fraudulent campaigns. In this paper, we aim to address this deficiency by collecting and analyzing publicly accessible web and social media data from a hundred fraudulent crowdfunding projects. In order to identify and comprehend the distinguishing characteristics of fraudulent campaigns, we first propose 1) using a wide variety of characteristics of campaign projects and project creators, including their profiles, behavior, social traits, and language; then, 2) we propose to use and combine three well-known multiple feature selection methods, which are based on Correlation-based Feature Selection (CFS), Pearson Correlation Coefficient (PCC), and Information Gain (IG), to identify representative features of fraudulent campaigns. Our approach identifies 10 commonly selected key features of fraudulent crowdfunding campaigns, three of which are new, original findings. We provide and discuss our findings and interpretations on the 10 commonly selected key features in relation to previous studies, based on which we construct a fraud detection model with 82.04% accuracy. We also employ Shapley Additive ExPlanations (SHAP) to interpret the fraud detection model, explaining the importance of each feature.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Fraud Detection</span>
        <span class="publication-tag">Crowdfunding</span>
        <span class="publication-tag">Multiple Feature Selection</span>
        <span class="publication-tag">Linguistic Features</span>
      </div>
    </div>
  </div>

  <!-- Fraud Detection MDPI Paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">Backers Beware: Characteristics and Detection of Fraudulent Crowdfunding Campaigns</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/Characteristics_and_Detection_of_Fraudulent_Crowdfunding_Campaigns.pdf" class="publication-button paper-button">Paper</a>
        <a href="https://doi.org/10.3390/s22197677" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Seung-hun Lee, Wafa Shafqat, and Hyun-chul Kim</p>
      <p class="publication-venue">Journal of MDPI Sensors, Volume 22, Number 19, pp. 7677, Oct. 2022.</p>
      <div class="publication-abstract">
        Crowdfunding has seen an enormous rise, becoming a new alternative funding source for emerging companies or new startups in recent years. As crowdfunding prevails, it is also under substantial risk of the occurrence of fraud. Though a growing number of articles indicate that crowdfunding scams are a new imminent threat to investors, little is known about them primarily due to the lack of measurement data collected from real scam cases. This paper fills the gap by collecting, labeling, and analyzing publicly available data of a hundred fraudulent campaigns on a crowdfunding platform. In order to find and understand distinguishing characteristics of crowdfunding scams, we propose to use a broad range of traits including project-based traits, project creator-based ones, and content-based ones such as linguistic cues and Named Entity Recognition features, etc. We then propose to use the feature selection method called Forward Stepwise Logistic Regression, through which 17 key discriminating features (including six original and hitherto unused ones) of scam campaigns are discovered. Based on the selected 17 key features, we present and discuss our findings and insights on distinguishing characteristics of crowdfunding scams, and build our scam detection model with 87.3% accuracy. We also explore the feasibility of early scam detection, building a model with 70.2% of classification accuracy right at the time of project launch. We discuss what features from which sections are more helpful for early scam detection on day 0 and thereafter.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Fraud Detection</span>
        <span class="publication-tag">Crowdfunding</span>
        <span class="publication-tag">Feature Selection</span>
        <span class="publication-tag">Logistic Regression</span>
        <span class="publication-tag">Linguistic Features</span>
      </div>
    </div>
  </div>

  <!-- Scam Detection Paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">Crowdfunding Scams : The Profiles and Language of Deceivers</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/Crowdfunding_Scams.pdf" class="publication-button paper-button">Paper</a>
        <a href="#" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Seung-hun Lee, and Hyun-chul Kim</p>
      <p class="publication-venue">Journal of The Korea Society of Computer and Information, Volume 23, Number 3, pp. 55-62, Mar. 2018.</p>
      <div class="publication-abstract">
        In this paper, we propose a model to detect crowdfunding scams, which have been reportedly occurring over the last several years, based on their project information and linguistic features. To this end, we first collect and analyze crowdfunding scam projects, and then reveal which specific project-related information and linguistic features are particularly useful in distinguishing scam projects from non-scams. Our proposed model built with the selected features and Random Forest machine learning algorithm can successfully detect scam campaigns with 84.46% accuracy.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Fraud Detection</span>
        <span class="publication-tag">Crowdfunding</span>
        <span class="publication-tag">Machine Learning</span>
        <span class="publication-tag">Linguistic cues</span>
      </div>
    </div>
  </div>

  <!-- Success Prediction Paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">Predicting Success of Crowdfunding Campaigns using Multimedia and Linguistic Features</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/Predicting_Success_of_Crowdfunding_Campaigns.pdf" class="publication-button paper-button">Paper</a>
        <a href="https://doi.org/10.9717/kmms.2018.21.2.281" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Kang-hee Lee, Seung-hun Lee, and Hyun-chul Kim</p>
      <p class="publication-venue">Journal of Korea Multimedia Society, Volume 21, Number 2, pp. 281-288, Feb. 2018.</p>
      <div class="publication-abstract">
        Crowdfunding has seen an enormous rise, becoming a new alternative funding source for emerging startup companies in recent years. Despite the huge success of crowdfunding, it has been reported that only around 40% of crowdfunding campaigns successfully raise the desired goal amount. The purpose of this study is to investigate key factors influencing successful fundraising on crowdfunding platforms. To this end, we mainly focus on contents of project campaigns, particularly their linguistic cues as well as multiple features extracted from project information and multimedia contents. We reveal which of these features are useful for predicting success of crowdfunding campaigns, and then build a predictive model based on those selected features. Our experimental results demonstrate that the built model predicts the success or failure of a crowdfunding campaign with 86.15% accuracy.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Success Prediction</span>
        <span class="publication-tag">Crowdfunding</span>
        <span class="publication-tag">Machine Learning</span>
        <span class="publication-tag">Linguistic Features</span>
        <span class="publication-tag">Multimedia Features</span>
      </div>
    </div>
  </div>

  <!-- Smart SNS Map paper -->
  <div class="publication-card">
    <div class="publication-info">
      <div class="publication-title-container">
        <h3 class="publication-title">Smart SNS Map: Location-based Social Network Service Data Mapping and Visualization System</h3>
        <a href="{{ root_url | prepend: site.baseurl}}/papers/Predicting_Success_of_Crowdfunding_Campaigns.pdf" class="publication-button paper-button">Paper</a>
        <a href="https://doi.org/10.9717/kmms.2016.19.2.428" class="publication-button doi-button">DOI</a>
      </div>
      <p class="publication-authors">Jangho Yoon, Seung-hun Lee, and Hyun-chul Kim</p>
      <p class="publication-venue">Journal of Korea Multimedia Society, Volume 19, Number 2, pp. 428-435, Feb. 2016.</p>
      <div class="publication-abstract">
        Hundreds of millions of new posts and information are being uploaded and propagated everyday on Online Social Networks(OSN) like Twitter, Facebook, or Instagram. This paper proposes and implements a GPS-location based SNS data mapping, analysis, and visualization system, called Smart SNS Map, which collects SNS data from Twitter and Instagram using hundreds of PlanetLab nodes distributed across the globe. Like no other previous systems, our system uniquely supports a variety of functions, including GPS-location based mapping of collected tweets and Instagram photos, keyword-based tweet or photo searching, real-time heat-map visualization of tweets and instagram photos, sentiment analysis, word cloud visualization, etc. Overall, a system like this, admittedly still in a prototype phase though, is expected to serve a role as a sort of social weather station sooner or later, which will help people understand what are happening around the SNS users, systems, society, and how they feel about them, as well as how they change over time and/or space.
      </div>
      <div class="publication-tags">
        <span class="publication-tag">Social Network Data Mapping</span>
        <span class="publication-tag">Location-based Visualization</span>
        <span class="publication-tag">Sentiment Analysis</span>
        <span class="publication-tag">Twitter</span>
      </div>
    </div>
  </div>
</div>


