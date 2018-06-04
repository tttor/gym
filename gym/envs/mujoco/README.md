# mujoco env

## Reacher-v2
* `done` is true when step_idx reaches `env.spec.timestep_limit`==50,
  * not when fingertip coincides with target position
  * the agent maintain its position once it has reach the target position
* reacher, where is env.spec.timestep_limit=50 per episode defined?
  * ans: /home/tor/ws-fork/gym@tttor/gym/envs/__init__.py
* standard reacher has frameskip(timestep skip)= 2
* action dim= 2 (for 2 joints)
* reacher ob.shape= 11
  * 2: sin(theta) of 2 joints
  * 2: cos(theta) of 2 joints
  * 2: qpos of target, x and y slide joints
  * 2: qvel of 2 joints
  * 3: distance between fingertip and target (3D cartesian)
* ? why set: reward_threshold=-3.75? instead of `=0`?
  is it sort of tolerance?
