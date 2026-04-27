---
layout: page
title: Benchmarking BC Algorithms in Robomimic
description: This project benchmarks different Behavior Cloning (BC) algorithms using the Robomimic framework 
img: assets/img/projects/bc1.png
importance: 6
category: "All"
date: 2025-12-20
---

### Introduction

This project is part of a broader study focused on evaluating Behavior Cloning (BC) algorithms. To benchmark these methods, I used the Robomimic framework with standardized datasets and a fixed manipulation task. The algorithms were evaluated on the Can PickPlace task (low_dim_v15.hdf5) using two datasets:

- Proficient-Human (PH): Collected by a single expert operator via the RoboTurk platform
- Multi-Human (MH): Collected by six different operators via RoboTurk

This setup allows for analyzing the impact of demonstration quality and diversity on model performance. All implementations and modifications are available in my forked [Github repository](https://github.com/pouyan-asg/robomimic).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc1.png" title="env" class="img-fluid rounded z-depth-1 mx-auto d-block" width="25%" %}
    </div>
</div>

To streamline experimentation, I created separate configuration files for each Behavior Cloning (BC) variant. These include: BC (Vanilla), BC-RNN (one- and two-layer architectures, with and without a recurrent GMM policy), BC-Transformer (with and without a GMM head). This setup enabled consistent and efficient comparison across different model architectures and training configurations. For more details on these algorithms, in addition to general resources, you can refer to the official [Robomimic documentation](https://robomimic.github.io/docs/introduction/implemented_algorithms.html). For more information, you can see the run time results for all algorithms on WandB wensite.


<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc2.png" title="BC algo names" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc3.png" title="Bc algo run time" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

All experiments were conducted under a consistent training setup to ensure fair comparison. Each model was trained for 1,000 epochs with a batch size of 100, using a fixed random seed. The Adam optimizer was employed with a learning rate of 0.0001.

For evaluation, each policy was tested over 50 rollout episodes, with a maximum horizon of 400 steps per episode, terminating either upon task completion or when the step limit was reached.

For more detailed configuration parameters and implementation details for each algorithm, please refer to the corresponding files in this [GitHub repository](https://github.com/pouyan-asg/robomimic/tree/master/robomimic/exps/templates).

### Results for MH dataset

In this section, the results are presented along with a detailed analysis of each method.

#### Train Losses

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/train/train_loss.png" title="Train Loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/train/train_loss_2.png" title="Train Loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/train/train_l1loss.png" title="L1 Loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/train/train_l2loss.png" title="L2 Loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/train/train_cosloss.png" title="Cos Loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/train/train_log_likelihood.png" title="Log Liklihood loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The figures above show the different loss values, where the training loss represents the combined loss of L1, L2, and cosine similarity terms.

**1.The "Negative Loss" Phenomenon (GMM Models):**

In the first Train/Loss graph, models such as BC_Transf_GMM and BC_RNN2_GMM reach values between -15 and -25. This behavior arises because stochastic policies (e.g., GMM-based models) in Robomimic do not rely on simple MSE loss. Instead, they optimize the Negative Log-Likelihood (NLL) of the expert actions.

When the model predicts a very sharp probability distribution (i.e., high precision and low variance) around the expert action, the likelihood can exceed 1. As a result, the log-likelihood becomes positive, and the NLL becomes negative.

Overall, BC_Transf_GMM (purple) achieves the lowest NLL, suggesting that it is the most confident model in capturing the distribution of the multi-human demonstrations.

**2.Comparative Regression Performance (L2, L1, and Cosine Loss):**

BC (Vanilla) consistently shows the highest error across L2, L1, and Cosine losses. This confirms that a simple MLP cannot capture the temporal dependencies or the complexity of the MH dataset. 

The BC_RNN2 (blue), which uses 2 layers and 400 hidden units, significantly outperforms the smaller 1-layer version (green). The extra capacity is clearly necessary to process the sequence data in the PickPlace task. 

The BC_Transf (brown) and BC_RNN2 (blue) are neck-and-neck in L1 and L2 losses, but BC_Transf shows a slight advantage in Cosine Loss. This suggests the Transformer is slightly better at predicting the direction of the robot's movement, even if the absolute coordinate error is similar to the RNN. 

**3.Log-Likelihood Trends** 

The Train/Log-Likelihood graph reflects the NLL results in reverse. The BC_Transf_GMM model achieves the highest log-likelihood (approximately 25), indicating strong alignment with the expert data.

All GMM-based models effectively learn a dominant mode of the human demonstrations. However, the Transformer's self-attention mechanism appears to capture and weight the multi-human data more effectively than the sequential bottleneck imposed by RNN-based models.

**Conclusion**

Based on these training curves, BC_Transf_GMM is expected to achieve the highest success rate during evaluation. However, caution is needed with BC_RNN2. Models that achieve very low L2 training loss may overfit to noise in the Multi-Human dataset, which can lead to poor handling of compounding errors during rollout.

#### Success Rate

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/successR/successrate.png" title="success rate" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/successR/successrate_mean.png" title="success rate mean" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/successR/successrate_std.png" title="success rate standard deviation" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The rollout success rate results clearly highlight the top-performing models in terms of generalization. Among all methods, BC_Transf_GMM emerges as the strongest performer, achieving a mean success rate of approximately 80%. This performance can be attributed to the Transformer architecture’s ability to capture long-range dependencies without the “forgetting” limitations of recurrent models. When combined with a Gaussian Mixture Model (GMM) policy, it effectively represents the diverse strategies present in the Multi-Human (MH) dataset, which includes demonstrations from multiple operators with varying levels of expertise.

A strong secondary performer is BC_Transf, which achieves a stable success rate of around 65%. Even without a GMM head, the Transformer’s global attention mechanism allows it to better handle the variability and noise in multi-human demonstrations compared to RNN-based approaches. Overall, the results consistently demonstrate a clear advantage of GMM-based policies across both RNN and Transformer architectures. This is expected, as the MH dataset is inherently multi-modal—different users complete the task using different strategies. Deterministic (vanilla) models tend to average these behaviors, often producing unrealistic intermediate actions that reduce success rates, whereas GMM-based models can represent multiple valid action modes.

A notable observation is the gap between training performance and real-world rollout success, particularly in the case of BC_RNN2. Despite achieving one of the lowest L2 training losses, its success rate plateaus at approximately 30%. This highlights a classic issue of covariate shift and compounding error. Since the model is deterministic and optimized using MSE loss, even small prediction errors during execution can push the system into states not seen during training. Without a probabilistic representation (such as GMM), the model struggles to recover, leading to poor performance despite strong training metrics.

Finally, analysis of the standard deviation and raw success rate plots reveals important insights into model stability. Several models, particularly BC_RNN2_GMM, exhibit high variance during early training stages. This behavior indicates that the policy occasionally discovers successful trajectories by chance before stabilizing. Similarly, BC_GMM shows significant variability, suggesting sensitivity to initial conditions and the specific mode selected during execution. These results highlight the trade-off between expressiveness and stability in stochastic policies, especially during early training phases.

#### Return

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/return/return.png" title="return" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/return/return_mean.png" title="return mean" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/return/return_std.png" title="return standard deviation" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The rollout return metric represents the total reward accumulated during an episode. In the Robomimic setup, this is typically defined as a sparse reward—where success yields a value of 1 and failure yields 0—or as a cumulative reward that penalizes longer trajectories. In this context, the return effectively reflects both task completion and efficiency.

Among all models, BC_Transf_GMM stands out as the most efficient performer. It achieves the highest mean return (approximately 0.8), which aligns with its top success rate. This indicates that the model is not only successful but also consistently completes the task in an efficient and stable manner across diverse multi-human demonstrations. When comparing the return and success rate curves, it becomes clear that they closely match, confirming that the environment uses a sparse reward structure where return is effectively equivalent to the probability of success.

In contrast, RNN-based models exhibit a noticeable performance gap. Even the best-performing RNN variant, BC_RNN_GMM, plateaus at a mean return of around 0.5. This significant gap—approximately 30% lower than the Transformer-based model—suggests that RNN architectures struggle to maintain consistent long-horizon planning. As a result, they are more prone to drifting away from the desired trajectory during the multi-step PickPlace task.

From a stability perspective, the standard deviation of returns provides additional insight into policy reliability. GMM-based models (e.g., BC_RNN2_GMM, BC_RNN_GMM, and BC_Transf_GMM) show relatively high variance during the early stages of training. This behavior is expected, as stochastic policies sample from a distribution, and early in training the model may select suboptimal modes before converging toward expert-like behaviors.

However, BC_RNN2_GMM exhibits consistently high variability even in later stages of training. This suggests that the model remains unstable, occasionally achieving successful rollouts but failing to generalize reliably. This instability likely arises from its inability to effectively separate and model the diverse strategies present in the Multi-Human dataset, leading to inconsistent performance across different episodes.

#### Horizon

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/horizon/horizon.png" title="horizon" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/horizon/horizon_mean.png" title="horizon mean" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/horizon/horizon_std.png" title="horizon std" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/horizon/time.png" title="time" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

In the Robomimic framework, the horizon represents the number of simulation steps taken before an episode terminates—either due to task success or reaching the maximum allowed step limit. As such, it serves as a proxy for efficiency: lower horizon values indicate faster and more direct task completion.

Among all models, BC_Transf_GMM stands out as the most efficient. It exhibits a clear downward trend in the mean horizon, stabilizing around approximately 240 steps. This behavior, combined with its high success rate, indicates that the model consistently reaches the goal using shorter and more optimal trajectories. It effectively captures efficient strategies from the demonstrations and avoids unnecessary hesitation during key phases such as grasping and placing.

In contrast, several models—including BC (vanilla) and BC_RNN variants—remain close to the maximum horizon range (approximately 350–400 steps). This pattern suggests that these models frequently fail to complete the task and instead continue executing actions until the time limit is reached. In practice, this often corresponds to inefficient behavior, such as wandering or getting stuck in suboptimal states (e.g., hovering over the object without completing the task).

The BC_Transf model (without GMM) also demonstrates a steady reduction in horizon over training, closely aligned with its increasing success rate. This further reinforces the advantage of Transformer-based architectures, which appear better suited for capturing long-horizon dependencies and executing tasks efficiently compared to the RNN-based models evaluated in this study.

#### System

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/system/GPU_usage.png" title="GPU usage" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/system/GPU_utilization.png" title="GPU utilization" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/system/GPU_utilization2.png" title="GPU utilization" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_mh/system/RAM.png" title="RAM" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The final results clearly show that, although Transformer-based models are significantly more computationally expensive, they are the only ones capable of fully mastering the Multi-Human (MH) PickPlace task. Their superior performance comes at the cost of higher resource usage and longer training times.

This trade-off is evident in the system performance metrics. The GPU utilization plots show that BC_Transf and BC_Transf_GMM consistently operate near 100% utilization. Unlike RNN-based models, which process sequences sequentially and are limited by step-by-step computation, Transformers leverage parallel processing across the entire sequence. This allows them to fully utilize GPU resources, but also results in higher demands for VRAM and computational power.

The difference is also reflected in training time. Based on the time (minutes) axis, Transformer models require nearly 250 minutes (over 4 hours) to reach 1,000 epochs, whereas simpler models complete training in less than half that time. This highlights a clear trade-off between computational efficiency and model performance: while Transformers demand more resources, they deliver significantly better results in complex, multi-modal tasks.

#### Final Thoughts

- Architecture Matters: The Transformer architecture is strictly superior to RNNs for this PickPlace task. The attention mechanism allows the robot to "re-index" its current stage (approach, grasp, lift) more reliably than a hidden state bottleneck. 

- Transformers are Mandatory: For the Multi-Human dataset, the Transformer's ability to model temporal relationships allows it to "plan" the PickPlace sequence without the drift seen in RNNs. 

- GMM is the Secret Sauce: The gap between BC_Transf (65%) and BC_Transf_gmm (80%) is exactly where the multi-modal nature of human operators lives. The GMM prevents the model from trying to perform an "average" of two different human strategies, which usually leads to a physical collision or miss. 

- High Std / Variance: The high standard deviation in the early epochs of the success and return graphs suggests that the models are sensitive to the initial object placement. 


### Results for PH dataset

In this section, the results are presented along with a detailed analysis of each method.

#### Train Losses

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/train/train_loss.png" title="Train Loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/train/train_loss_2.png" title="Train Loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/train/train_l1loss.png" title="L1 Loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/train/train_l2loss.png" title="L2 Loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/train/train_cosloss.png" title="Cos Loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/train/train_log_likelihood.png" title="Log Liklihood loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The training loss results show a consistent advantage for GMM-based models, particularly when using high-quality demonstrations. In both the Train/Loss and Train/Log-Likelihood curves, stochastic models demonstrate significantly stronger performance. Among them, BC_Transf_GMM_PH achieves the highest log-likelihood (approximately 27.5) and the lowest negative log-likelihood (around −27.5). This behavior reflects the model’s ability to assign very high probability to expert actions. Since the Proficient-Human (PH) dataset is highly consistent and largely unimodal, the model can concentrate its predictions around a single dominant strategy. As a result, the likelihood becomes very sharp, leading to strongly negative NLL values. The rapid drop in loss during early epochs further indicates that the Transformer quickly captures the underlying task structure.

Across architectures, a clear ranking emerges: Transformer-based models outperform RNN-based models, with RNN2 performing better than single-layer RNNs. This trend holds even when the data quality is high, confirming that the Transformer's ability to model long-range dependencies provides a structural advantage for sequential tasks such as PickPlace.

For deterministic models, the regression-based losses (L1, L2, and cosine) show more stable and lower error values compared to the multi-human experiments. In particular, BC_Transf_PH achieves the lowest L2 (~0.005) and L1 (~0.002) losses, demonstrating its ability to closely match expert actions. This improvement is largely due to the clarity of the PH dataset, where a consistent “ground truth” trajectory exists. The Transformer's global attention mechanism enables precise mapping from observed states to actions with minimal noise.

A comparison between recurrent models shows that BC_RNN2_PH performs significantly better than BC_RNN_PH, approaching Transformer-level performance. This suggests that when data quality is high, model capacity—such as depth and number of units—plays a critical role alongside architectural design. Interestingly, even the vanilla BC model (MLP) performs relatively well in this setting. Although it still has the highest loss among the tested models, its L2 error (~0.02) is lower than that of some RNN models trained on the multi-human dataset, highlighting the strong influence of data quality on learning outcomes.

Finally, the cosine loss results provide insight into directional accuracy. Both BC_Transf_PH and BC_RNN2_PH achieve very low cosine loss values (below 0.05), indicating that the predicted action vectors closely match the direction of expert actions. This is particularly important for phases such as reaching and placing, where precise motion direction is critical for task success.

#### Success Rate

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/successR/successrate.png" title="success rate" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/successR/successrate_mean.png" title="success rate mean" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/successR/successrate_std.png" title="success rate standard deviation" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The rollout success rates on the Proficient-Human (PH) dataset show a substantial improvement across all architectures compared to the Multi-Human (MH) results. This highlights a key insight: high-quality, consistent demonstrations significantly simplify the learning problem for imitation learning models. With reduced variability in the data, models can more easily learn a stable and effective policy.

In the success rate curves, most models achieve between 80% and 100% success, a clear contrast to the MH setting where only the best Transformer model approached 80%. Notably, BC_RNN_PH emerges as a strong performer, maintaining success rates close to 90–100% throughout training. This can be explained by the unimodal nature of the PH dataset. Since all demonstrations come from a single expert, the RNN does not need to resolve conflicting strategies and can reliably map sequences of observations to a consistent action trajectory.

The overall model ranking also shifts in this setting. BC_RNN_PH and BC_Transf_GMM_PH both perform at the top level, demonstrating that when the data is clean and consistent, even simpler sequential models can match the performance of more complex architectures. Meanwhile, BC_RNN2_PH and BC_Transf_PH stabilize around 80% success. Interestingly, the deeper RNN (RNN2) performs slightly worse than the single-layer version, suggesting that with very clean data, additional model capacity may lead to mild overfitting to subtle variations in the demonstrations. On the lower end, BC_GMM_PH and the vanilla BC_PH model lag behind, indicating that temporal context—provided by RNNs or Transformers—remains essential for solving sequential tasks like PickPlace, even with high-quality data.

From a stability perspective, the standard deviation of success rates provides insight into policy reliability. BC_Transf_GMM_PH demonstrates the most stable behavior, with a low and decreasing variance (~0.1), indicating consistent performance across different initial conditions. In contrast, models such as BC_GMM_PH and BC_RNN2_GMM_PH exhibit higher variability (~0.3), suggesting sensitivity to initial states or instability in sampling from the learned action distribution. This reinforces the advantage of Transformer-based architectures in not only achieving high performance but also maintaining consistent and reliable behavior.

#### Return

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/return/return.png" title="return" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/return/return_mean.png" title="return mean" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/return/return_std.png" title="return standard deviation" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The rollout return results on the Proficient-Human (PH) dataset provide strong confirmation that the models have effectively mastered the task. Since this dataset consists of consistent, high-quality demonstrations from a single operator, the achievable performance is significantly higher than in the Multi-Human (MH) setting. In this context, the return metric closely aligns with success rate, as the environment uses a sparse reward structure.

The results show near-perfect performance for the top models. Both BC_RNN_PH and BC_Transf_GMM_PH reach mean returns close to 1.0, indicating that they succeed in nearly every rollout. Interestingly, the single-layer BC_RNN_PH is among the fastest to converge to this level of performance. This behavior can be explained by the unimodal nature of the PH dataset: since all demonstrations follow a consistent strategy, the RNN can effectively learn and generalize a single execution pattern without being affected by conflicting trajectories. In contrast to its performance on the MH dataset, the RNN no longer struggles with hidden state ambiguity and can maintain stable execution.

Transformer-based models also demonstrate strong and consistent performance. Both BC_Transf_PH and BC_Transf_GMM_PH show stable convergence toward high returns, highlighting the robustness of the self-attention mechanism. Even in a simplified data setting, Transformers maintain reliable performance and do not suffer from the limitations observed in recurrent architectures under more complex conditions.

From a stability perspective, the standard deviation of returns provides additional insight into policy reliability. For the top-performing models, particularly BC_RNN_PH and BC_Transf_GMM_PH, the variance decreases toward zero as training progresses. This indicates that the models are not succeeding by chance, but have learned a consistent and repeatable policy that performs reliably across different initial conditions.

In contrast, GMM-based models exhibit higher variance during the early stages of training. This is expected, as these models sample from a learned distribution of actions. Before the distribution converges to well-defined modes, the model may occasionally select suboptimal actions, resulting in temporary drops in return. However, as training progresses and the policy stabilizes, this variability decreases significantly.

#### Horizon

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/horizon/horizon.png" title="horizon" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/horizon/horizon_mean.png" title="horizon mean" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/horizon/horizon_std.png" title="horizon std" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/horizon/time.png" title="time" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The rollout horizon results provide a clear view of task efficiency, as the horizon represents the number of simulation steps required to complete an episode. In the Proficient-Human (PH) setting, the improvements in efficiency are significantly more pronounced than in the Multi-Human (MH) experiments, reflecting the benefit of consistent and high-quality demonstrations.

Among all models, BC_RNN_PH and BC_Transf_GMM_PH emerge as the most efficient performers. Both exhibit a steady and rapid decrease in mean horizon, eventually stabilizing between 150 and 200 steps. This indicates that these models have successfully captured the expert’s optimal strategy, allowing them to complete the task using shorter and more direct trajectories. Rather than merely achieving success, they consistently reach the goal with minimal unnecessary motion, reflecting strong learning of the underlying task structure.

In contrast, models such as BC_PH (vanilla) and BC_RNN_GMM_PH maintain higher average horizons, around 300 steps. Despite being trained on high-quality data, these models struggle with smooth transitions between task phases, such as moving from grasping to lifting. As a result, they tend to spend additional time in intermediate states—often exhibiting small oscillations or hesitation—before completing the task, leading to longer episode durations.

The execution time analysis further supports these findings. Most of the top-performing models in the PH setting complete their tasks within 3 to 5 seconds, which is a noticeable improvement compared to the MH experiments, where completion times were typically between 6 and 8 seconds. In particular, BC_RNN_PH demonstrates both high speed and consistency. Its relatively lightweight architecture enables fast per-step inference, and its ability to follow a learned optimal trajectory allows it to terminate episodes quickly upon success.

From a reliability perspective, the standard deviation of the horizon highlights differences in model consistency. BC_Transf_GMM_PH shows the lowest variance toward the end of training, indicating highly consistent behavior across different episodes. Once trained, it follows a near-deterministic and efficient trajectory regardless of variations in initial conditions. In contrast, models such as BC_GMM_PH exhibit much higher variability, with standard deviations reaching up to ~80 steps. This suggests that while they may occasionally find efficient solutions, they often deviate from optimal paths, making them less reliable for tasks that require precision and repeatability.

#### System

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/system/GPU_usage.png" title="GPU usage" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/system/GPU_utilization.png" title="GPU utilization" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/system/GPU_utilization2.png" title="GPU utilization" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/BCs_ph/system/RAM.png" title="RAM" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The computational analysis highlights a clear trade-off between performance and efficiency across model architectures. Transformer-based models, including BC_Transf and BC_Transf_GMM, require significantly more time to reach 1,000 training epochs—approximately 250 minutes, compared to 100–150 minutes for RNN-based models. This difference stems from the fundamental nature of the architectures. While RNNs process sequences sequentially with linear complexity, Transformers rely on self-attention mechanisms that process entire sequences in parallel. Although this enables better utilization of GPU parallelism, it introduces quadratic memory and computational complexity, leading to substantially higher demands in terms of FLOPs and VRAM.

An interesting observation is the difference in system behavior between the PH and MH datasets. The hardware utilization metrics for the PH experiments are noticeably smoother, suggesting more stable gradient updates and less time spent dealing with noisy or conflicting data. This results in more consistent training dynamics and improved overall efficiency at the system level.

GPU utilization patterns further illustrate the architectural differences. Transformer models maintain near-constant GPU saturation, with utilization close to 100% and power usage around 80% throughout training. This indicates that their performance is primarily limited by the throughput of large matrix operations in the self-attention layers. In contrast, RNN-based models exhibit more irregular, “spiky” GPU utilization. Due to their sequential processing nature, portions of the GPU often remain idle while waiting for step-by-step computations to complete, resulting in lower overall resource usage but reduced computational efficiency.

From a memory and batch-processing perspective, Transformer models also incur higher costs. System RAM usage for the PH experiments peaks at around 3 GB, which is manageable for low-dimensional inputs but is expected to scale significantly when using image-based observations, where sequence representations become much larger. Additionally, batch processing time for Transformers is approximately twice as long as that of simpler BC or RNN models, reflecting the overhead of attention computations and larger intermediate representations.

#### Final Thoughts

**1.Multi-Human (MH) Dataset Analysis**

* The MH dataset consists of demonstrations from six different operators of varying proficiency, introducing significant noise and multi-modality. 

    - Training Dynamics: Stochastic models (GMM) achieved negative loss values (~-25), indicating high confidence in capturing complex human distributions. Deterministic models (Vanilla BC) showed the highest reconstruction errors, as they struggled to "average" conflicting human strategies. 

    - Success & Returns: BC_Transf_gmm was the clear leader, peaking at ~80% success. RNN-based models (like BC_RNN2) suffered from a massive performance gap—despite low training loss, they plateaus at ~30% success due to "compounding error" and a lack of distribution-modeling capability. 

    - Efficiency: The Transformer-GMM was the most efficient, completing tasks in ~240 steps. Lower-performing models often "timed out" near the maximum step limit of 400. 

    - System Cost: Transformer models required the most resources, maintaining nearly 100% GPU utilization and taking roughly 250 minutes to train. 

**2.Proficient-Human (PH) Dataset Analysis**

* The PH dataset features 200 consistent trajectories from a single professional operator, providing a cleaner learning signal. 

    - Training Dynamics: Models reached higher log-likelihoods (~27.5) and lower absolute L2 errors (~0.005) compared to MH. The unimodal nature of the data allowed for much sharper convergence. 

    - Success & Returns: Multiple models, including BC_RNN and BC_Transf_gmm, reached near-perfect performance (90–100% success). This highlighted a "redemption" for RNNs, which failed on noisy MH data but excelled on consistent PH data. 

    - Efficiency: The best models reached the goal significantly faster than in MH tests, with horizons dropping to 150–200 steps. Path execution was highly direct with minimal "jitter". 

    - System Cost: While Transformers remained more computationally expensive, the hardware utilization was smoother due to more consistent gradients from the high-quality demonstrations. 


### Comparision for BC and BC_RNN

For a clearer comparison, three common Behavior Cloning (BC) variants were evaluated across both Proficient-Human (PH) and Multi-Human (MH) scenarios: BC (vanilla), BC-RNN (single layer), and BC-RNN (two layers). These models are widely used as baseline policies in human-in-the-loop approaches such as DAgger and its variants, although a detailed discussion of these methods is beyond the scope of this project.

While a full one-to-one comparison across all configurations was not completed, the overall trend is clear. Across nearly all models, the PH dataset consistently yields better performance than the MH dataset. This is reflected in lower training losses, higher success rates, and improved returns. The results reinforce the importance of data quality and consistency in imitation learning: models trained on single-expert (unimodal) data are able to learn more stable and efficient policies compared to those trained on multi-operator (multi-modal) demonstrations.

#### BC Vanilla

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC/l1loss.png" title="L1 loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC/l2loss.png" title="L2 loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC/horizon.png" title="Horizon" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC/cosloss.png" title="Cos loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC/return.png" title="Return" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC/successrate.png" title="Succes rate" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### BC RNN (one layer)

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC_RNN/l1loss.png" title="L1 loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC_RNN/l2loss.png" title="L2 loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC_RNN/horizon.png" title="Horizon" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC_RNN/cosloss.png" title="Cos loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC_RNN/return.png" title="Return" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC_RNN/successrate.png" title="Succes rate" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### BC RNN (two layer)

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC_RNN2/return.png" title="Return" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/bc_results/comparisons/BC_RNN2/successrate.png" title="Succes rate" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Reference

A valuable reference for understanding which parameters most influence imitation learning algorithms is this paper (*[What Matters in Learning from Offline Human Demonstrations for Robot Manipulation](https://arxiv.org/abs/2108.03298)*). The authors evaluate different scenarios across multiple algorithms, providing insightful analysis and practical observations.

Key insights from the paper:

- Human data is not Markovian: History plays an important role, making temporal models (e.g., RNNs, Transformers) more effective.
- Multi-human data is noisy: Variations in skill and strategy can reduce learning performance.
- Dataset size matters: Larger datasets improve results, but collecting human demonstrations can be costly.
- Training loss ≠ real performance: Low training loss does not necessarily translate to high success rates, making proper evaluation essential.
