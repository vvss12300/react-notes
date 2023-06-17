# React Components #
- Components
	Breaking the app in smaller pieces called components
- JSX
	- Writting html code in Javascript
	- Converted in JS during app building
 - Props
	- Passing data from parent component to child component
```JS
const Tool = (props) => {
  const name = props.name;
  const tool = props.tool;
    return (
      <div>
        <h1>My name is {name}.</h1>
        <p>My favorite design tool is {tool}.</p>
      </div>
    );
}
```
- Props Drilling
	- Prop drilling in react is the process of passing data from one component via several interconnected components to the component that needs it.
	![Alt text](/Images/Prop%20Drilling.jpg?raw=true "Optional Title")
- Event Handlers (onClick or OnBlur)
- Lifting the State Up
- 2 way Binding
- Rendering Lists and Improtance of Keys prop
- Refs
- Forward Refs
- Controlled vs UnControlled components
- React Fragements (Wrapper Components) <></>
- React portals
- React Context - Context Store, Provider, Consumer

Styling:
- Inline using style prop
- className prop
- Styled Components
- CSS Modules

Hooks + Side Effects
- Only call React Hooks in React Functions

- const [firstName, setFirstName] = useSate('')
- useEffect(() = {}, [<dependencies>])
- useReducer(<initialState>, <actionFunction/reducerFunction>)
- useContext(<store>)
- useCallback() - Preventing Function Re-Creation
- useMemo() Optimizing of component 
- custom Hooks - Outsource stateful logic into re-usefal functions
- useSelector - React Redux hook to get state snapshot
- useStore - React Redux hook to manage store
- useDispatch - React Redux hook to dispatch actions from components
- useParams - React Router hook to fetch the params
- useHistory - React Router hook to manage page location 
- useLocation - React Router hook to get current page details like url and query parameters
- useNavigate - React Router V6 hook for navigation replacing useHistory
- useLoaderData - React Router V6.4 hook for getting the loader data defined in Route loader prop
- useRouteError - React Router V6.4 hook used to get error returned during routing

Lifecycle
- Mounting : constructor(), getDerivedStateFromProps(), render(), and componentDidMount()
- Updating : shouldComponentUpdate(), render(), getSnapshotBeforeUpdate() and componentDidUpdate()
- Unmounting : componentWillUnmount
- componentDidCatch

Function vs Class Components
   function Sample() {
     return <h2>Hello World!</h2>;
   }
   
   class Sample extends React.Component {
     render() {
       return <h2>Hi, I am a Car!</h2>;
     }
   }

Debugging:
- React Dev Tools

Redux 
- Read about flux as well
- Cross Component or App Wide State Management
- Context API is not for high frequency state propation, thats why Redux is preffered 
- How it works: Conponents dispatch actions that get forwarded to Reduce function which changes the state
- const store = redux.createStore(reducer)
- reducerFunction(currentState, action){}
- Subscribe: store.subscribe(<subscriptionfunction>);

- Attaching in React App
	- npm install redux react-redux
	- Wrap parent component with <Provider store={store}><App/></Provider>
	- use in compenent const counter = useSelector(state => state.counter)
	- Dispatch actions:
		- const dispatch = useDispatch();
		- dispatch({type:'ABC', paylod: <payloadData>})
- Class based components
	- connect(<mapStateToProps>, <mapDispatchToProps>)(<Component>)
- Don't mutate the state in reducer

- Redux Toolkit
	- Makes the redux setup easier
	- npm install @reduxjs/toolkit
	- createSlice - to prepare slices of store
		- const counterSlice = createSlice({
				name: 'Slice1',
				initialState: { counter: 0, showCounter: true},
				reducers: {
					increment(state) {},
					decrement(state) {},
				}
			})
	- const store = configureStore({
		reducer: counterSlice.reducer
		});
	- export counterSlice.actions;
	- In the component
		- import {counterActions}
		- dispatch(counterActions.increment()) //can pass payload in the argument
	- Split multiple slices in multiple files
	
- Async Code with Redux
	- Don't do in reducer function as it doesn't support side effects
	- Two options
		1. Do in components using useEffect
		2. Action Creators
			- Thunk - A function that delays an action until later
			- An action creator returns anther function which eventually returns the action
				export const sendCartData = (cart) => {
					return async (dispatch) => {					
					
						const sendRequest = async () => {
						const response = await fetch(
							'https://react-http-6b4a6.firebaseio.com/cart.json',
							{
							method: 'PUT',
							body: JSON.stringify(cart),
							}
						);
					
						if (!response.ok) {
							throw new Error('Sending cart data failed.');
						}
						};
					
						try {
						await sendRequest();				
						} catch (error) {
						dispatch(
							uiActions.showNotification({
							status: 'error',
							title: 'Error!',
							message: 'Sending cart data failed!',
							})
						);
						}
					};
				};
	- Redux DevTools

React Router (version 5)
- Create different routes in the app
- Render client side web page based on route
- Install
	- npm install react-router-dom
- version 5 is widely used. New version 6 is also out

- Setup 
	- Go to index.js
		- import {BrowserRouter} from 'react-router-dom';
		- root.render(<BrowserRouter><App/></BrowserRouter>);
	- Go to App.js
		- import {Route} from 'react-router-dom'
		- <Route path="/page1"><Page1Component/></Route>
		  <Route path="/page2"><Page2Component/></Route>

- Link Component
	- use to create links to switch between routes without browser reload
	- import {Link} from 'react-router-dom'
	- <Link to='/page1'>Page 1</Link>
- NavLink Component
	- to set the active link class name
	- <NavLink activeClassName={classes.active} to='/page1'>Page 1</NavLink>

- Passing params in routes
	- <Route path="/page1/:someParam"><Page1Component/></Route>
	- In the component 
		import {useParams} from 'react-router-dom'
		const params = useParams();
		{params.someParam}
- Switch Component: to match only one route 
- exact prop: to match exact path
- Nested Routes: Routes can defined in child components and will be evaluated when component is loaded in DOM
- Redirct Component
	- import {Redirect} from 'react-router-dom'
	- <Route path="/" extact><Redirect to='/page1'/></Route>
- NotFound Page
	-   <Route path='*'><NotFoundCompnent></Route>
- Pragamattically navigating
	- const history = useHistory()
	- history.push(<location of new page>)
	- history.replace(<location of new page>)
	- push keeps the history and clicking back user can come back to this page while replace doesn't
- Prompt Component
	- To prevent accidental navigation
- Read QueryString Paramters
	- useLocation: current page details like url and query parameters
	- const location = useLocation();
	  var queryParams = new URLSearchParams(location.search);
- useMatch hook
	- to get the route data like path, params, exact
	

React Router (version 6)
- Switch is replaced by Routes
- Component to be rendered to be specified in element prop instead of child element
	- <Route path="/page1" element={<Page1Component/>}></Route>
- exact prop is removed and matching exact path became default behaviour
- activeClassName is removed from NavLink
	- instead use className which also get navData
	- className={(navData) => navData.isActive ? classes.active : ''}
- Riderect is replaced by Navigate
- Nested Router
	- Need to wrap route in child component with Routes
	- Also routes in child component will be relative
	- Like if parent is page1 and nested in page1/detailed
	- then only define detailed in child component
	- Same applies to Links
- Outlet: to define where nested route defined in main route page will be loading in child component
- useHistory is replacted by useNavigate
	- const navigate = useNavigate();
	  navigate('/page2')
	  or
	  navigate(<-1/1>) : to moveforward or backward in history


React Router (version 6.4)
- Some ground breaking features for data fetching
- new "loader" prop is introduced in Route
	- we can data loading function to that loader prop
	- it can be an array or promise
	- <Route path='/BlogPosts' element={<BlogPosts/>} loader={loadBlogPosts}/>
	- useLoaderData hook to get data in component 
	- Read about createBrowserRoute and createRoutesFromElement
	- errorElement is introduced to render content if error occured
	- useRouteError hook is used to get error returned during routing
- new "action" prop to send data to server
	- useActionData hook to get action response
- defer
	- for defering loading data
	- page will loaded and then loading request will be sent


Deploying Apps
- Test, Build Production Bundle, Setup Server, Deploy
- Lazy Loading
	- React.lazy: support dynamic import loading
	  const NewQuote = React.lazy(() => import('./pages/NewQuote'))
	- Suspense component
		- Make React aware lazy loading the component
		- <Suspense fallback={<fallback element>}>
		  <Child Component>
		  </Suspense>
	- each lazy load import is bundled in seperate chunk and loaded on demand
- run npm build to create a build bundle
- it calls "react-scripts build" internally
- build folder contains all the files need to deployed on server
- For SPA with client side routing, configure the server to rewrite all urls to index.html

Animate React Apps
- Native CSS transitions and animations can be used in the CSS files
	-  using (transition + transform) and keyframes
	- Limitation is that Component is always in the DOM to perform animations

- react-transition-group
	-3rd party lib to perform animations in React
	- import Transition from 'react-transition-group/Transition'
	  <Transition 
	  in={showControl} timeout={1000}
	  mountOnEnter unmountOnExit>
	  {state => (
		<div style={{<animations>}}></div>
	  )}
	  </Transition>
	




