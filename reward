prev_progress = 0
def reward_function(params):
    global prev_progress

    # Read all input parameters
    progress = max(0, params['progress'])
    steps = params['steps']
    speed = params['speed']
    steering_angle = params['steering_angle']
    is_offtrack = params['is_offtrack']

    # Reward - make progress as fast as possible
    prog_per_step = max(0, ((progress / steps) ** 3) * 5)
    prog_diff = max(0, progress - prev_progress)
    reward = prog_per_step + prog_diff

    # Additional reward for faster speed at lesser steering
    if abs(steering_angle) < 10 and speed >= 2.5:
        reward *= 1.3
    elif abs(steering_angle) < 20 and speed >= 1.7:
        reward *= 1.1

    # Start at faster speed as we are starting from Zero
    if steps < 5 and speed >= 2.5:
        reward *= 1.3
    elif steps < 10 and speed >= 1.7:
        reward *= 1.1

    ## Zero reward if off track ##
    if is_offtrack:
        reward = 1e-7

    prev_progress = progress
    return float(reward)
