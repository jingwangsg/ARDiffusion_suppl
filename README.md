## Baseline Results

<div align="center">
<table>
  <tr>
    <th>Context Length</th>
    <th>Method</th>
    <th>Memory Budget</th>
    <th>0-16</th>
    <th>16-48</th>
    <th>overall</th>
  </tr>
  <tr>
    <td>48</td>
    <td>Prepending Memory + Memory Compression (Ours)</td>
    <td>16</td>
    <td>0.36</td>
    <td>0.25</td>
    <td>0.31</td>
  </tr>
  <tr>
    <td>48</td>
    <td>FIFO Diffusion [1]</td>
    <td>16</td>
    <td>0.12</td>
    <td>0.03</td>
    <td>0.075</td>
  </tr>
  <tr>
    <td>48</td>
    <td>Outpainting</td>
    <td>16</td>
    <td>0.10</td>
    <td>0.02</td>
    <td>0.06</td>
  </tr>
  <tr>
    <td>48</td>
    <td>Prepend Memory + Last 16 Frames [2]</td>
    <td>16</td>
    <td>0.42</td>
    <td>0.00</td>
    <td>0.21</td>
  </tr>
  <tr>
    <td>48</td>
    <td>Prepend Memory + Last 32 Frames with 1 Frame Skip [2]</td>
    <td>16</td>
    <td>0.23</td>
    <td>0.15</td>
    <td>0.19</td>
  </tr>
  <tr>
    <td>48</td>
    <td>GameNGen [3]</td>
    <td>16</td>
    <td>0.14</td>
    <td>0.00</td>
    <td>0.07</td>
  </tr>
</table>
</div>

<center><div style="width: 800px; font-size: 1.2em; text-align: left"><b>Table 1. Baseline Results across Multiple Frame Conditioning Strategies. </b>Context Length refers to the number of raw frames used as prior observations (i.e., memory). By default, we use a default Context Length of 48 frames, along with an additional 16 frames for generating the output—except for GameNGen, which generates one frame at a time. To ensure a fair comparison, we constrain all methods to a memory budget of 16 frames. Accordingly, we either sample 16 frames from the 48-frame context or compress the 32 context frames into an equivalent number of tokens corresponding to 16 frames. </div></center>

<br>
[1] Jihwan Kim, Junoh Kang, Jinyoung Choi, Bohyung Han. FIFO-Diffusion: Generating Infinite Videos from Text without Training. NeurIPS 2024
<br>
[2] William Harvey, Saeid Naderiparizi, Vaden Masrani, Christian Weilbach, Frank Wood. Flexible Diffusion Modeling of Long Videos. NeurIPS 2022
<br>
[3] Dani Valevski, Yaniv Leviathan, Moab Arar, Shlomi Fruchter. Diffusion Models Are Real-Time Game Engines, 2024

## Insights from Error Term Decompositions

<center><img src="assets/pretrained_error.png" alt="Timestep Scheduling" width="1000"/></center>
<center><div style="width: 800px; font-size: 1.2em; text-align: left"><b>Fig 1. Error Term Decomposition of Pretrained Model. </b>We calculate the MSE loss across different timesteps of the pretrained models. The loss is accumulated across the entire MSR-VTT dataset and reported as the average loss.</div></center>

<br>

<center><img src="assets/fvd_comparison_timestep_scheduling.png" alt="Timestep Scheduling" width="1000"/></center>

<center><div style="width: 800px; font-size: 1.2em; text-align: left"><b>Fig 2. Error Accumulation using Different Timestep Scheduling. </b>This demonstrates the error accumulation of OpenSoraPlan+FIFO with different time steps schedulers. We consider the schedule that is $\text{Uniform}([0,999^{\alpha}] )^{1/\alpha}$. Here we set $\alpha$ as $1/2$ (order 2) and $1/3$ (order 3). The ``reverse'' refers to the schedule that is $999 - \text{Uniform}([0,999^{\alpha}] )^{1/\alpha}$</div></center>

## More Visualizations

### Successful Cases from Minecraft

<center><img src="assets/minecraft_demo.png" alt="Minecraft Demo" width="1000"/></center>
<center><div style="width: 800px"><b>Fig 3. Minecraft Demo. </b>The left frames represent the expected ground truth, while the right frames, outlined with a red square, are generated by the model. The first 4 frames without red squares are provided context.</div></center>

### Raw Videos from Minecraft

<div style="display: flex; justify-content: space-between;">
  <video width="48%" controls>
    <source src="assets/minecraft_demos/minecraft_success_minerlbasaltbuildvillagehouse_v0_20016.mp4" type="video/mp4">
  </video>
  <video width="48%" controls>
    <source src="assets/minecraft_demos/minecraft_success_minerlbasaltbuildvillagehouse_v0_20051.mp4" type="video/mp4">
  </video>
</div>
