# Animations

Although a graph is a very useful tool to visualize a simulation, sometimes it's more insightful to make an animation. Matplotlib offers the possibility to create animations using `matplotlib.animation`. It gives a multitude of possibilities to create movement. We will demonstrate a small example, in which we create an animated .gif of a moving dot along $$f(x)=sin(x)$$. 

## A moving dot

When you draw a point (one $$x$$-value and one $$y$$-value) of which the $$x$$ and $$y$$ change over time, then the point appears to move over the screen. In the code below we let $$x$$ increment, calculate $$y$$ and draw the point on the screen. We also use commands `xlim` and `ylim` to specify in the plot what $$x$$-values and $$y$$-values we want to display.

    import math
    import matplotlib.pyplot as plt
    from matplotlib.animation import FuncAnimation, PillowWriter

    def update(frame):
        """This update function will be automatically called by FuncAnimation() below
        We use the 'frame' parameter to determine how far along we are in the animation: 
        - the first time the function is called, the 'frame' parameter is 0
        - it is increased by one on each succesive call of `update()`
        """
        
        # clear graph
        ax.clear()  
        
        # use small steps of 0.05 for x
        x = frame / 20 
        
        # compute corresponding y value
        y = math.sin(x) 

        # plot graph
        ax.plot(x, y, 'bo', markersize = 10)
        plt.xlim(0, 2 * math.pi)
        plt.ylim(-1, 1)

        # update graph
        plt.draw()
        plt.pause(0.001)

        return ax

    # start plot
    fig, ax = plt.subplots()

    # Create animation
    print("animate...")
    ani = FuncAnimation(fig, update, frames=130, blit=False)

    # Save animation as .gif (this might take a good minute)
    print("save gif...")
    ani.save("sine.gif", writer=PillowWriter(fps=20))
    print("done!")

![](../../assets/AnimationExampleSin1.gif)

* As you can see, we use the function `update()` in our code. This function is called repeatedly by `FuncAnimation()` (once for each frame). The `frame` paramater is automatically set by `FuncAnimation()` to indicate the frame number. So we can use that to know how far along the animation we are.
* The function `ani.save()` is used to save the collection of frames as an animated gif. You can use this to 
* Run the code for yourself and play around with it.
    * What happens when you remove the `ax.clear()`?
    * What happens when you change `x = frame / 20` into `x = frame / 40`?
