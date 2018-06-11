# mujoco env

## Reacher-v2
* `done` is true when step_idx reaches `env.spec.timestep_limit`==50,
  * not when fingertip coincides with target position
  * the agent maintain its position once it has reach the target position
  * ? where is this coded?
```
# @/home/tor/ws/gym/gym/wrappers/time_limit.py
def step(self, action):
    print('@time_limit: step')
    assert self._episode_started_at is not None, "Cannot call env.step() before calling reset()"
    observation, reward, done, info = self.env.step(action)
    self._elapsed_steps += 1

    if self._past_limit():
        if self.metadata.get('semantics.autoreset'):
            _ = self.reset() # automatically reset the env
        done = True

    return observation, reward, done, info
```

* where is env.spec.timestep_limit=50 per episode defined?
  * ans: `gym/gym/envs/__init__.py`
* standard reacher has frameskip(timestep skip)= 2
* action dim= 2 (for 2 joints)
* reacher ob.shape= 11
  * 2: sin(theta) of 2 joints
  * 2: cos(theta) of 2 joints
  * 2: qpos of target, x and y slide joints
  * 2: qvel of 2 joints
  * 3: distance between fingertip and target (3D cartesian)
* diff seed make diff target pose,
  and init jointpos, which is random in [-0.1, +0.1) rad (~5.72 deg)

* ? why set: reward_threshold=-3.75? instead of `=0`?
  is it sort of tolerance?
