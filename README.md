# redux-react-hook-main
# Yarn
yarn add redux-react-hook

# NPM
npm install --save redux-react-hook

//
// Bootstrap your app
//
import {StoreContext} from 'redux-react-hook';

ReactDOM.render(
  <StoreContext.Provider value={store}>
    <App />
  </StoreContext.Provider>,
  document.getElementById('root'),
);

//
// Individual components
//
import {useDispatch, useMappedState} from 'redux-react-hook';
import shallowEqual from 'shallowequal';

export function DeleteButton({index}) {
  // Declare your memoized mapState function
  const mapState = useCallback(
    state => ({
      canDelete: state.todos[index].canDelete,
      name: state.todos[index].name,
    }),
    [index],
  );

  // Get data from and subscribe to the store
  const {canDelete, name} = useMappedState(mapState, shallowEqual);

  // Create actions
  const dispatch = useDispatch();
  const deleteTodo = useCallback(
    () =>
      dispatch({
        type: 'delete todo',
        index,
      }),
    [index],
  );

  return (
    <button disabled={!canDelete} onClick={deleteTodo}>
      Delete {name}
    </button>
  );
}
