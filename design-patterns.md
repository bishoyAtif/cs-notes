# OOP Design

### Service Locator

Many developers out there don’t see the difference between the dependency injection and the service locator design patterns. Yes, both of them are trying to solve the same problem — increase decoupling. We all know what benefits this give us when it comes to scaling, testing or simply reading the code.
However, how do I know when to use dependency injection and when to use service locator? I would say we should use both of them when appropriate.
If I was asked to choose a single verb that best describes the dependency injection pattern I would choose “to give”. If you think about it, that’s exactly what we achieve with dependency injection after all. We simply give objects to an object.
$window = new Window();
$door = new Door();
$house = new House($window, $door);
In this case, we give the window object and the door object to the house object.
On the other hand, if I was asked to describe the service locator pattern with a single verb I would say “to take”. Just think about it. That’s what we do when we use a service locator. We take objects from an object.
$house = $serviceLocator->get(House::class); 
As you can see, we take the house object from the service locator.
In many cases, the dependency injection and the service locator work as a single unit. We might not see it when the things are injected automagically but behind the scene the implementations of dependency injection rely on service locators in order to retrieve actual dependencies.
This is how it might look like somewhere in the code:
foreach ($dependencies as $dependency) {
    $instances[] = $this->container->get($dependency);
}
return $this->resolve($class, $instances);
A service locator is pretty easy to implement. All you need is to have ability to get a requested instance by name or id and ability to check whether the requested instance actually exists. Worth to note that a service locator is often called a container. Both things are the same. Both of them are meant to provide instances or services however you prefer to call them. Of course, there’s a difference between a service and an instance when speaking about terms and purposes, but from the technical point of view they are all instances of certain classes.
Here’s a primitive version of a service locator (aka container):
class ServiceLocator {

    private $services = [];

    public function get(string $id) : ?object {
        return $this->services[$id] ?? null;
    }


    public function has(string $id) : bool {
        return isset($this->services[$id]);
    }

    public function register(string $id, object $service) : void {
        $this->services[$id] = $service;
    }
}
$serviceLocator = new ServiceLocator();
$serviceLocator->register('house', new House());
// somewhere else

if ($serviceLocator->has('house')){
    $house = $serviceLocator->get('house');
}
Additionally, I have provided the way to register services.
The implementations of dependency injection usually inject dependencies into objects automatically. All you need is to provide a bit of configuration and that’s all. That’s pretty convenient in many cases, but there are cases when you have to use service locator to avoid the deadlock. This could happen when two instances are depended on each other via constructor. Here’s an example:
class A {
    
    public function __construct(B $b)
    {
        //
    }
}

class B {
    public function __construct(A $a)
    {
        //
    }
}
$a = new A(...); // We need B!
$b = new B(...); // We need A!
As you can see, we cannot resolve any of the services because they are depended on each other. We cannot resolve the service A because it requires the service B, and we cannot resolve the service B because it requires the service A. To solve this, we need to retrieve one of the services in lazy-loading way. Meaning that, we should take one of the services from the service locator at the point when the service is actually needed and not in the constructor.
All in all
Hope this article cleared some things up for you and you enjoyed reading it. If not, then you must be already smartest programer out there ;-)