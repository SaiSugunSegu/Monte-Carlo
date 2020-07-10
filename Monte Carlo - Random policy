import gym
import numpy as np
import matplotlib.pyplot as pyplot

e=0.9
gamma=1
env = gym.make('Blackjack-v0')

sum_attribute = np.array(range(0,32))
dealer_attribute = np.array(range(1,11))
ace_attribute = [False, True]
action_space = [0,1]

q = {}
state_space = []
returns = {}
state_action_count = {}

for total in sum_attribute:
    for card in dealer_attribute:
        for ace in ace_attribute:
            for action in action_space:
                q[((total, card, ace), action)] = 0
                returns[((total, card, ace), action)] = 0
                state_action_count[((total, card, ace), action)] = 0
            state_space.append((total, card, ace))
            
            
def sample_policy():
    action = env.action_space.sample()
    return action
    
            
def episode(env):
    states = []
    actions = []
    rewards = []
    state = env.reset()
    while True:
        action = sample_policy()
        next_state, reward, done, info = env.step(action)
        
        states.append(state)
        states.reverse()
        actions.append(action)
        actions.reverse()
        rewards.append(reward)
        rewards.reverse()
        
        state = next_state
        if done:
            break
    return states, actions, rewards


  def monte_carlo_first_visit(episodes):
    for i in range(episodes):
        states, actions, rewards = episode(env)    
        g = 0
        for t in range(len(states)):
            s = states[t]
            a = actions[t]
            r = rewards[t]
        
            g += gamma*g + r
        
            p = (s,a)
        
            state_action_first_visit=[]
            
            if p not in state_action_first_visit:
                state_action_count[(p)] += 1
                #print('count:',state_action_count[(p)])                          # incremental implementation
                returns[(p)] += (1/state_action_count[(p)]) * (g-returns[(p)])   # new estimate = 1 / N * [sample - old estimate]
                q[(p)] = returns[(p)]
            
            state_action_first_visit.append(p)


monte_carlo_first_visit(100000)


for total in range(12,22):
    for card in range(1,11):
        for ace in ace_attribute:
            for action in action_space:
                print("q ({},{}): {}".format((total, card, ace),action,q[((total, card, ace), action)]))



 def plot_blackjack(V, ax1, ax2):
    X, Y = np.meshgrid(player_sum, dealer_show)
    ax1.plot_wireframe(X, Y, v[:, :, 0])   
    ax2.plot_wireframe(X, Y, v[:, :, 1])
    for ax in ax1, ax2:   
        ax.set_zlim(-1, 1)
        ax.set_ylabel('Player_sum')
        ax.set_xlabel('Dealer_sum')
        ax.set_zlabel('state_value')
fig, axes = pyplot.subplots(nrows=2, figsize=(5, 8),subplot_kw={'projection': '3d'})
axes[0].set_title('state-value distribution w/o usable ace')
axes[1].set_title('state-value distribution w/ usable ace')
plot_blackjack(value, axes[0], axes[1])           
            
            
            
            
            
            
            
            
            
