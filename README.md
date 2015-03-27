# Singleton-Pattorn
For installing Unity directly You can use command in package manager console PM> Install-Package Unity -Version 3.5.1404
or you can download its dll from  http://www.microsoft.com/en-in/download/details.aspx?id=38788

check steps for creating singleton pattern 
 /// <summary>
    /// this is singleton pattern using to one time initalization of the object
    /// </summary>
    public class ObjectLocator
    {
        //1)-> we have to make private static readoly object
        private static readonly IUnityContainer objectContainer = new UnityContainer();

        /// <summary>
        /// 2)->private static instance of the class
        /// </summary>
        private static ObjectLocator _instance;

        /// <summary>
        ///3)-> private constructor for access provision not allow to create an object of the class 
        /// </summary>
        private ObjectLocator()
        {
        }

        //4)->get static property to geting instance to class
        public static ObjectLocator Instance
        {
            get
            {
                if(_instance == null)
                {
                    _instance = new ObjectLocator();
                }
                return _instance;
            }
        }

       
        /// <summary>
        ///  5)->genric  method to declare to givin access to method using class name .intance.method name
        /// </summary>
        /// <typeparam name="T">For the typcast of the function by developer sent on runtime</typeparam>
        /// <returns></returns>
        public T GetService<T>() where T : class
        {
            return objectContainer.Resolve<T>();
        }

        public void RegisterService<T>() where T : class
        {
            objectContainer.RegisterType<T>(new ContainerControlledLifetimeManager());
        }
    }
