# React component

## Function component

```TS
import React, { useEffect } from "react";
import { makeStyles, createStyles, Theme } from "@material-ui/core/styles";

//--- Mui Styles override
const useStyles = makeStyles((theme: Theme) =>
	createStyles({
		//Set your style
	})
);

//--- IProps & IState
interface IProps {}
interface IState {}

//--- Component
export function MuiFunctionComponent(props: IProps) {
	//Mui
	const classes = useStyles(props);

	//--- Init state
	const initSate: IState = {};
	const [state, setState] = React.useState<IState>(initSate);

	//Replace lifecycle with hooks
	useEffect(() => console.log("mounted"), []);
	useEffect(() => console.log("mounted or updated"));
	useEffect(() => {
		return () => {
			console.log("will unmount");
		};
	}, []);

	return <div>function component</div>;
}
```

## Class component

```TS
import React from "react";
import { withStyles, createStyles, Theme, withTheme, WithStyles, WithTheme } from "@material-ui/core";

//--- Mui Styles override
const styles = (theme: Theme) =>
	createStyles({
		//Set your style
	});

//IProps & IState
interface IProps {}
type AllProps = IProps & WithStyles<typeof styles> & WithTheme;
interface IState {}

//--- Component
class MuiClassComponentBase extends React.Component<AllProps, IState> {

	public readonly state: Readonly<IState> = {};

	constructor(props: AllProps) {
		super(props);
	}

	public async componentDidMount() {
		console.log("componentDidMount");
	}

	public async componentDidUpdate() {
		console.log("componentDidUpdate");
	}

	public async componentWillUnmount() {
		console.log("componentWillUnmount");
	}

	public render() {
		const { classes } = this.props;
		const { theme } = this.props;
		return <div>class component</div>;
	}
}

export const MuiClassComponent = withTheme(withStyles(styles)(MuiClassComponentBase));
```
